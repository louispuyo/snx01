# snx01

# 🔐 Rapport de Pentest – OWASP Juice Shop

## 📅 Informations générales
- **Application testée** : OWASP Juice Shop
- **Environnement** : AWS EC2 (t2.micro, Ubuntu + Docker)
- **Date du test** : JJ/MM/AAAA
- **Testeur** : [Ton Nom / Pseudo]
- **Durée** : [X jours/heures]

---

## 🎯 Objectifs du test
- Identifier les vulnérabilités de l’application (OWASP Top 10).
- Évaluer les risques de compromission.
- Fournir des recommandations de sécurité.
- Observer les logs et détections côté AWS (CloudTrail, GuardDuty).

---

## 🛠️ Méthodologie
- **Reconnaissance** : nmap, whatweb, analyse DNS.
- **Analyse automatique** : OWASP ZAP, Nikto.
- **Tests manuels** : Burp Suite, injection manuelle, fuzzing.
- **Audit AWS** : IAM, Security Groups, S3, CloudTrail/GuardDuty.
- **Référentiel** : [OWASP Top 10](https://owasp.org/Top10/)

---

## 🔎 Résumé des vulnérabilités
| ID | Vulnérabilité | Gravité | Statut |
|----|---------------|---------|--------|
| VULN-01 | SQL Injection (Login) | 🔴 Élevée | Trouvée |
| VULN-02 | XSS Reflected (Search) | 🟠 Moyenne | Trouvée |
| VULN-03 | IDOR (User Profile) | 🔴 Élevée | En cours |
| VULN-04 | JWT Manipulation | 🟠 Moyenne | Non testé |
| VULN-05 | Sensitive Data Exposure (/ftp) | 🟢 Faible | Trouvée |

---

## 📂 Détails des vulnérabilités

### VULN-01 – SQL Injection (Login)
- **Description** : L’application n’échappe pas correctement les entrées utilisateur lors de l’authentification.  
- **Preuve (PoC)** :  

→ Connexion réussie sans mot de passe.  
- **Impact** : Accès non autorisé, compromission du compte administrateur.  
- **Gravité** : 🔴 Élevée  
- **Recommandation** :  
- Utiliser des requêtes préparées (paramétrées).  
- Valider les entrées utilisateur.  
- Mettre en place un WAF.  

---

### VULN-02 – XSS Reflected (Search)
- **Description** : Le champ recherche reflète directement les entrées utilisateur.  
- **Preuve (PoC)** :  
```html
<script>alert("xss")</script>