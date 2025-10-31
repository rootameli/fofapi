# Outils de recherche et de vérification FOFA & ZoomEye

> Ensemble d'outils en ligne de commande pour rechercher, valider et gérer des clés API FOFA et ZoomEye.

## 🌟 Principales fonctionnalités

- 🔍 **Double prise en charge** : compatibilité avec les plateformes FOFA et ZoomEye.
- 🚀 **Recherche automatisée** : exploration de GitHub (et autres sources démo) à la recherche de clés divulguées.
- ✅ **Vérification en masse** : contrôle automatique de la validité des API et filtrage des entrées obsolètes.
- 📊 **Informations détaillées** : récupération des soldes, statuts VIP, quotas restants, etc.
- 🎯 **Contrôle fin** : limitation ou mode illimité du nombre de fichiers analysés.
- 🔄 **Déduplication intelligente** : chaque fichier est traité une seule fois afin de limiter les appels.
- 💾 **Sauvegarde automatique** : enregistrement des API valides au format JSON.
- 🎨 **Interface CLI colorée** : progression lisible et messages explicites.
- ⚙️ **Fichier de configuration** : paramètres persistants pour les jetons GitHub et les options réseau.
- 🖥️ **Scripts batch Windows** : lancement simplifié via menu pour les utilisateurs Windows.

## 📁 Structure du projet

```
fofapi/
├── fofa_api_searcher.py         # Recherche d'API FOFA
├── fofa_api_tool.py             # Vérification d'API FOFA
├── zoomeye_api_searcher.py      # Recherche d'API ZoomEye
├── zoomeye_api_tool.py          # Vérification d'API ZoomEye
├── config.py                    # Gestion du fichier de configuration
├── config.ini                   # Exemple de configuration
├── requirements.txt             # Dépendances Python
├── run_all.bat                  # Menu Windows unifié
├── run_fofa.bat                 # Lancement rapide FOFA
├── run_zoomeye.bat              # Lancement rapide ZoomEye
├── found_fofa_apis.txt          # Résultats bruts FOFA
├── found_zoomeye_apis.txt       # Résultats bruts ZoomEye
├── valid_fofa_apis.json         # API FOFA valides
└── valid_zoomeye_apis.json      # API ZoomEye valides
```

## 🚀 Mise en route

### Prérequis

- Python 3.6+
- `requests`
- `urllib3`

### Installation

```bash
# 1. Cloner ou télécharger le dépôt
git clone <url_du_depot>
cd fofapi

# 2. Installer les dépendances
pip install -r requirements.txt

# 3. (Optionnel) Configurer un jeton GitHub
# Modifier config.ini et renseigner votre token
```

### Mode graphique (Windows)

```bash
# Double-cliquer
run_all.bat

# Suivre les indications du menu :
# 1. Choisir la plateforme (FOFA ou ZoomEye)
# 2. Choisir l'action (recherche, vérification ou flux complet)
# 3. Indiquer le nombre de fichiers à analyser (Entrée = valeur par défaut)
```

### Utilisation en ligne de commande

#### Outils FOFA

```bash
# Recherche (20 fichiers par défaut)
python fofa_api_searcher.py

# Recherche de 100 fichiers
python fofa_api_searcher.py --max-results 100

# Mode illimité
python fofa_api_searcher.py --max-results 0

# Avec jeton GitHub (fortement recommandé)
python fofa_api_searcher.py --github-token VOTRE_TOKEN --max-results 100

# Vérifier les API trouvées
python fofa_api_tool.py -f found_fofa_apis.txt --test-query
```

#### Outils ZoomEye

```bash
# Recherche (20 fichiers par défaut)
python zoomeye_api_searcher.py

# Recherche de 200 fichiers
python zoomeye_api_searcher.py --max-results 200

# Mode illimité
python zoomeye_api_searcher.py --max-results 0

# Avec jeton GitHub
python zoomeye_api_searcher.py --github-token VOTRE_TOKEN --max-results 200

# Vérifier les API trouvées
python zoomeye_api_tool.py -f found_zoomeye_apis.txt --test-query
```

## 📖 Guide d'utilisation détaillé

### 1. Outils FOFA

#### Recherche (`fofa_api_searcher.py`)

```bash
# Recherche avec configuration par défaut
python fofa_api_searcher.py

# Limiter le nombre de fichiers analysés
python fofa_api_searcher.py --max-results 100

# Mode illimité (analyse de tous les fichiers trouvés)
python fofa_api_searcher.py --max-results 0

# Utiliser un jeton GitHub
python fofa_api_searcher.py --github-token VOTRE_TOKEN --max-results 200

# Définir un fichier de sortie
python fofa_api_searcher.py -o mes_apis.json --max-results 100

# Recherche uniquement sur GitHub
python fofa_api_searcher.py --github-only --max-results 50
```

Options avancées :

```bash
# Désactiver la vérification SSL (non recommandé)
python fofa_api_searcher.py --no-verify-ssl

# Modifier le délai réseau
python fofa_api_searcher.py --timeout 60

# Générer un fichier de configuration
python fofa_api_searcher.py --create-config
```

#### Vérification (`fofa_api_tool.py`)

```bash
# Mode interactif (recommandé pour débuter)
python fofa_api_tool.py

# Vérifier une API unique
python fofa_api_tool.py -e votre@email.com -k votre_cle_api

# Vérification en masse
python fofa_api_tool.py -f found_fofa_apis.txt

# Vérification + test de requête
python fofa_api_tool.py -f found_fofa_apis.txt --test-query

# Spécifier un fichier de sortie
python fofa_api_tool.py -f found_fofa_apis.txt -o apis_valides.json
```

### 2. Outils ZoomEye

#### Recherche (`zoomeye_api_searcher.py`)

```bash
python zoomeye_api_searcher.py
python zoomeye_api_searcher.py --max-results 200
python zoomeye_api_searcher.py --max-results 0
python zoomeye_api_searcher.py --github-token VOTRE_TOKEN --max-results 200
```

#### Vérification (`zoomeye_api_tool.py`)

```bash
python zoomeye_api_tool.py
python zoomeye_api_tool.py -k votre_cle_api
python zoomeye_api_tool.py -f found_zoomeye_apis.txt --test-query
```

### 3. Scénario complet

```bash
# FOFA
python fofa_api_searcher.py --github-token VOTRE_TOKEN --max-results 100 -o found_fofa_apis.txt
python fofa_api_tool.py -f found_fofa_apis.txt --test-query

# ZoomEye
python zoomeye_api_searcher.py --github-token VOTRE_TOKEN --max-results 200 -o found_zoomeye_apis.txt
python zoomeye_api_tool.py -f found_zoomeye_apis.txt --test-query

# Résultats valides :
# - valid_fofa_apis.json
# - valid_zoomeye_apis.json
```

## ⚙️ Configuration (`config.ini`)

```ini
[github]
# Jeton personnel GitHub utilisé pour la recherche
token = votre_token_github

[search]
# Nombre maximal de fichiers (0 = illimité)
default_max_results = 100
# Délai réseau en secondes
default_timeout = 30

[api]
# Identifiants FOFA optionnels
email =
key =

[network]
# Vérification SSL
verify_ssl = false
# Nombre maximal de tentatives
max_retries = 2
```

### Obtenir un jeton GitHub

1. Rendez-vous sur <https://github.com/settings/tokens>
2. Cliquer sur **Generate new token (classic)**
3. Sélectionner au minimum la permission `public_repo`
4. Générer puis copier le jeton
5. Le renseigner dans `config.ini`

**Pourquoi ?** Sans authentification, GitHub limite à 60 requêtes/heure, contre 5000 avec un jeton.

## 📊 Fichiers de sortie

### FOFA

- **found_fofa_apis.txt / .json** : liste brute (non vérifiée)
- **valid_fofa_apis.json** : API valides avec détails

```json
[
    {
        "email": "example@example.com",
        "key": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
        "username": "user123",
        "fcoin": 48,
        "isvip": true,
        "vip_level": 1,
        "remain_api_query": 10000,
        "remain_api_data": 10000,
        "verified_at": "2025-10-11 12:34:56"
    }
]
```

### ZoomEye

- **found_zoomeye_apis.txt / .json** : liste brute
- **valid_zoomeye_apis.json** : API valides détaillées

```json
[
    {
        "api_key": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
        "username": "user123",
        "email": "example@example.com",
        "role": "developer",
        "quota": {
            "remain_free_quota": 10000,
            "total_quota": 10000
        },
        "verified_at": "2025-10-11 12:34:56"
    }
]
```

## 💡 Conseils pratiques

### Choisir le nombre de fichiers

| Valeur | Effet | Durée estimée | Usage conseillé |
| ------ | ----- | ------------- | --------------- |
| 20 (défaut) | 20 fichiers | 2-5 min | Tests rapides |
| 50 | 50 fichiers | 5-10 min | Utilisation courante |
| 100 | 100 fichiers | 10-15 min | Recommandé ✓ |
| 200 | 200 fichiers | 15-25 min | Recherche approfondie |
| 0 | illimité | 30-50 min | Analyse exhaustive |

### Optimiser les performances

1. **Configurer un jeton GitHub** — essentiel pour éviter les limites API.
2. **Ajuster le nombre de fichiers** — inutile de viser trop haut si les résultats sont suffisants.
3. **Mode illimité** — utile lors de la première exploration.
4. **Connexion stable** — éviter les coupures réseau prolongées.
5. **Scripts batch** — pour une utilisation simplifiée sous Windows.

### Stratégies proposées

- **Validation rapide**
  ```bash
  python fofa_api_searcher.py --max-results 20
  python fofa_api_tool.py -f found_fofa_apis.txt --test-query
  ```
- **Recherche standard**
  ```bash
  python fofa_api_searcher.py --max-results 100
  python fofa_api_tool.py -f found_fofa_apis.txt --test-query
  ```
- **Recherche exhaustive**
  ```bash
  python fofa_api_searcher.py --max-results 0
  python fofa_api_tool.py -f found_fofa_apis.txt --test-query
  ```
- **Combinaison FOFA + ZoomEye**
  ```bash
  python fofa_api_searcher.py --max-results 100
  python zoomeye_api_searcher.py --max-results 200
  python fofa_api_tool.py -f found_fofa_apis.txt --test-query
  python zoomeye_api_tool.py -f found_zoomeye_apis.txt --test-query
  ```

## ❓ FAQ

### FOFA vs ZoomEye ?
- **FOFA** nécessite un couple e-mail + clé, développé par Baimaohui.
- **ZoomEye** repose sur une clé unique (UUID), édité par 404 Laboratory.
- Les deux moteurs ont des sources différentes : explorer les deux maximise les chances de succès.

### Comment augmenter le nombre de fichiers analysés ?
```bash
python fofa_api_searcher.py --max-results 200
# ou modifier config.ini :
[search]
default_max_results = 200
```

### Pourquoi aucun résultat ?
1. Jeton GitHub absent ⇒ limite très rapide.
2. Problèmes réseau.
3. Mots-clés insuffisants (les scripts incluent plusieurs requêtes).
4. Peu de fuites publiques ⇒ normal.

**Solutions :** fournir un jeton GitHub, augmenter `--max-results`, utiliser le mode illimité.

### Erreurs lors de la vérification ?
- Clé expirée ou révoquée.
- Problème réseau.
- Service FOFA/ZoomEye indisponible temporairement.
- Adresse ou clé au mauvais format.

### Pourquoi « 30/100 fichiers traités » ?
- 30 = nombre de fichiers récupérés pour cette requête.
- 100 = objectif global défini par l'utilisateur.
- Plusieurs requêtes sont enchaînées pour atteindre la cible.

### Exécuter la recherche en arrière-plan ?
```bash
# Windows
start /B python fofa_api_searcher.py --max-results 0

# Linux / macOS
nohup python fofa_api_searcher.py --max-results 0 &
```

### Erreur SSL ?
```bash
python fofa_api_searcher.py --no-verify-ssl
```
*(À n'utiliser qu'en dernier recours.)*

## ⚠️ Avertissements

1. Outils destinés à l'apprentissage et à la recherche.
2. Respect de la vie privée : les API trouvées peuvent appartenir à des tiers.
3. Respecter les CGU de FOFA et ZoomEye.
4. Attention aux quotas et limites API.
5. Configurer un jeton GitHub pour éviter les blocages.
6. Maintenir une connexion stable.

### Performance

- Dépend du réseau et du nombre de fichiers.
- L'API GitHub impose un taux maximal (5000/h authentifié).
- Les duplications sont évitées pour gagner du temps.

### Protection des données sensibles

- Ne jamais publier `config.ini` avec un jeton actif.
- Utiliser `.gitignore` si le dépôt est public.

## 🔧 Dépannage

- **Limites GitHub** : fournir un jeton, patienter une heure ou réduire la fréquence.
- **Timeout réseau** : augmenter `--timeout`.
- **Fichier introuvable** : vérifier le répertoire et exécuter la recherche avant la vérification.

## 📈 Notes de version

### v1.2 (2025-10-11)
- Correction du traitement en double et respect du quota cible.
- Mode illimité (`--max-results 0`).
- Scripts batch améliorés.
- Progression plus lisible et gains de performances (~50 %).

### v1.1 (2025-10-11)
- Ajout des outils ZoomEye (recherche + vérification).
- Documentation enrichie.
- Script `run_all.bat` ajouté.

### v1.0 (2025-10-11)
- Version initiale : recherche FOFA, vérification, gestion de configuration et mode interactif.

## 📄 Licence

Utilisation réservée à des objectifs éducatifs et de recherche. L'utilisateur reste responsable de toute utilisation abusive.

## 📣 Support

1. Consulter la FAQ ci-dessus.
2. Vérifier la configuration (`config.ini`).
3. S'assurer que toutes les dépendances sont installées.
4. Ouvrir une issue avec un descriptif précis.

## 🔗 Liens utiles

- [FOFA](https://fofa.info/)
- [ZoomEye](https://www.zoomeye.org/)
- [Paramètres des jetons GitHub](https://github.com/settings/tokens)

---

**Version** : v1.2  
**Auteur** : dafebgche  
**Dernière mise à jour** : 11 octobre 2025  

⭐ Si ce projet vous est utile, pensez à laisser une étoile !
