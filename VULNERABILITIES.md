# Rapport de vulnérabilités

# Semgrep | Rapport de vulnérabilités - app.py

Le scan Semgrep a détecté **8 findings bloquants** dans `app.py`. Certains fichiers ont été partiellement analysés en raison d’erreurs de parsing ou internes. Le scan était limité aux fichiers suivis par Git.

---

## 1. Utilisation dangereuse de `eval`
- **Règles détectées** :  
  - `python.django.security.injection.code.user-eval.user-eval`  
  - `python.flask.security.injection.user-eval.eval-injection`  
  - `python.lang.security.audit.eval-detected.eval-detected`
- **Description** : L'application utilise `eval()` sur des données utilisateurs, permettant l'exécution de code arbitraire.  
- **Détails** : [Semgrep - eval user input](https://sg.run/PJDW), [Semgrep - eval injection](https://sg.run/5QpX), [Semgrep - eval detected](https://sg.run/ZvrD)  
- **Recommandation** : Supprimer l'utilisation de `eval()` sur des entrées externes. Utiliser des bibliothèques sécurisées comme `asteval` ou `numexpr`, ou un parser personnalisé.

---

## 2. App Flask exposé publiquement
- **Règle détectée** : `python.flask.security.audit.app-run-param-config.avoid_app_run_with_bad_host`  
- **Description** : L'application est exécutée avec `host='0.0.0.0'`, ce qui la rend accessible publiquement.  
- **Détails** : [Semgrep - Flask host](https://sg.run/eLby)  
- **Recommandation** : Limiter l'accès à `127.0.0.1` en développement ou utiliser un reverse proxy sécurisé en production.

---

## 3. Debug activé en production
- **Règle détectée** : `python.flask.security.audit.debug-enabled.debug-enabled`  
- **Description** : `debug=True` est actif, exposant potentiellement des informations sensibles et un shell interactif.  
- **Détails** : [Semgrep - Flask debug](https://sg.run/dKrd)  
- **Recommandation** : Désactiver `debug=True` en production et gérer le mode debug via des variables d’environnement.

---

## 4. Clé secrète codée en dur
- **Règle détectée** : `python.flask.security.audit.hardcoded-config.avoid_hardcoded_config_SECRET_KEY`  
- **Description** : La variable `SECRET_KEY` est codée en dur, ce qui peut compromettre la sécurité des sessions et la protection CSRF.  
- **Détails** : [Semgrep - SECRET_KEY](https://sg.run/Ekde)  
- **Recommandation** : Stocker les secrets dans des variables d’environnement ou des fichiers de configuration sécurisés.

---

## 5. Template string vulnérable
- **Règle détectée** : `python.flask.security.audit.render-template-string.render-template-string`  
- **Description** : Utilisation de `render_template_string` avec du formatage direct, exposant à des injections de template côté serveur (SSTI) et à des attaques XSS.  
- **Détails** : [Semgrep - Template string](https://sg.run/8yjE)  
- **Recommandation** : Utiliser `render_template` avec des fichiers `.html` séparés et ne jamais injecter directement des données utilisateur.

---

## 6. Injection NaN dans les castings
- **Règle détectée** : `python.flask.security.injection.nan-injection.nan-injection`  
- **Description** : Les entrées utilisateur sont castées directement avec `float()`, `bool()` ou `complex()`, permettant l’injection de valeurs NaN et un comportement indéfini.  
- **Détails** : [Semgrep - NaN injection](https://sg.run/e598)  
- **Recommandation** : Valider et filtrer les entrées avant conversion. Ajouter des contrôles pour empêcher l’injection de NaN.

---

# Snyk | Vulnérabilités dans les dépendances (requirements.txt)

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
