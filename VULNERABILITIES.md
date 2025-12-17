# Rapport de vulnérabilités (mise à jour limitée)

## Snyk | Vulnérabilités dans les dépendances (requirements.txt)

### Flask 2.0.1 → 2.2.5
- **Vulnérabilité :** Information Exposure  
- **CVSS :** 7.5 (High)  
- **Lien Snyk :** [SNYK-PYTHON-FLASK-5490129](https://security.snyk.io/vuln/SNYK-PYTHON-FLASK-5490129)  
- **Introduit par :** flask@2.0.1  
- **Action recommandée :** Mettre à jour flask vers 2.2.5  

### Requests 2.25.0 → 2.32.4
- **Insertion d’infos sensibles**  
  - CVSS : 5.7 (Medium)  
  - [Lien Snyk](https://security.snyk.io/vuln/SNYK-PYTHON-REQUESTS-10305723)  
  - Introduit par : requests@2.25.0  

- **Information Exposure**  
  - CVSS : 6.1 (Medium)  
  - [Lien Snyk](https://security.snyk.io/vuln/SNYK-PYTHON-REQUESTS-5595532)  
  - Introduit par : requests@2.25.0  

- **Contrôle de flux incorrect**  
  - CVSS : 5.6 (Medium)  
  - [Lien Snyk](https://security.snyk.io/vuln/SNYK-PYTHON-REQUESTS-6928867)  
  - Introduit par : requests@2.25.0  

- **Risque lié aux dépendances** (résolu indirectement via update de requests) :  
  - `idna 2.10` → `3.7` : Resource Exhaustion, CVSS 6.2  
    - [Lien Snyk](https://security.snyk.io/vuln/SNYK-PYTHON-IDNA-6597975)  
    - Introduit par : requests@2.25.0 > idna@2.10  

  - `urllib3 1.26.20` → `2.6.0` :  
    - Open Redirect, CVSS 6.0, [Lien Snyk](https://security.snyk.io/vuln/SNYK-PYTHON-URLLIB3-10390194)  
    - Data Amplification, CVSS 8.9, [Lien Snyk](https://security.snyk.io/vuln/SNYK-PYTHON-URLLIB3-14192442)  
    - Allocation sans limites, CVSS 8.8, [Lien Snyk](https://security.snyk.io/vuln/SNYK-PYTHON-URLLIB3-14192443)  
    - Introduit par : requests@2.25.0 > urllib3@1.26.20  

**Action recommandée :** Mettre à jour requests vers 2.32.4
