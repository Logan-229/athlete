# ATHLETE 0.1 — Application de suivi sportif locale

## Contenu
- `index.html` : interface et logique JavaScript/CSS sans bibliothèques externes.
- `manifest.json` : configuration d'installation PWA.
- `service-worker.js` : cache du shell applicatif pour usage hors ligne.
- `icons/` : icônes.

## Utilisation sur Windows (développement)
1. Décompresser l'archive ATHLETE.
2. Ouvrir PowerShell dans le dossier `ATHLETE`.
3. Saisir `py -m http.server 8000` (Python requis).
4. Ouvrir `http://localhost:8000` dans Chrome ou Edge.
5. Dans le menu du navigateur, choisir **Installer ATHLETE** si l'option apparaît.
6. Après le premier chargement avec connexion, l'application et les données locales restent disponibles hors ligne sur ce même appareil/profil de navigateur.

Ne pas simplement ouvrir `index.html` par double-clic pour tester la PWA : les service workers exigent HTTPS ou localhost.

## Installation sur Android / Honor
1. Publier **tout le dossier** en site statique HTTPS (par exemple GitHub Pages, Cloudflare Pages ou Netlify). Les fichiers de l'application sont publics, mais **les données sportives restent uniquement dans ton navigateur**.
2. Ouvrir l'adresse HTTPS depuis Chrome sur le téléphone.
3. Menu ⋮ > **Ajouter à l'écran d'accueil** ou **Installer l'application**.
4. Ouvrir une première fois l'application en étant connecté, puis tester le mode avion.

GitHub Pages : créer un dépôt avec ces fichiers à la racine, aller dans Settings > Pages > Deploy from a branch > main / root. Le site HTTPS fourni par GitHub sera l'adresse de l'application. Ne jamais committer les fichiers de sauvegarde JSON personnels.

## Guide rapide
- **Dashboard** : suivi de la semaine, objectifs, records et état de forme ; flèches pour organiser les blocs.
- **Calendrier** : vue semaine/mois/liste, planning récurrent et fiches.
- **Séances** : choisir un sport, renseigner les données et le statut, enregistrer ; modèles disponibles.
- **Stats** : bilans hebdomadaires/mensuels et historiques de course et musculation.
- **Objectifs/Records** : ajout et validation manuels.
- **Récupération** : fatigue, douleur et forme.
- **Paramètres** : profil de référence, thème, préférences et exports.

## Sauvegardes et confidentialité
Les informations sont enregistrées dans IndexedDB, associé à l'origine (URL) du site et au profil du navigateur. Ne pas vider les données du site sans sauvegarde. ATHLETE conserve jusqu'à 30 instantanés quotidiens locaux, créés quand l'application est ouverte. Ce n'est **pas** une sauvegarde externe.

Dans Paramètres :
- **Sauvegarde complète JSON** : fichier portable et versionné.
- **Importer / restaurer** : sélection des catégories et fusion sans remplacer les entrées de même ID. Copie de sécurité préalable.
- **Exporter Excel** : `.xlsx` avec plusieurs feuilles de données.
- **Rapport PDF mensuel** : ouvre une fenêtre d'impression ; choisir « Enregistrer au format PDF ».

## Limites connues de cette version 0.1
- Les notifications ne sont vérifiées que lorsque l'application est active/ramenée au premier plan ; pas de rappel garanti lorsque le navigateur est fermé.
- Pas de synchronisation entre appareils : exporter/importer les sauvegardes manuellement.
- Les statistiques avancées de progression, la détection d'anomalies et les comparaisons personnalisées demandent encore des améliorations.
- Le sélecteur d'unités impériales est conservé comme préférence, mais la conversion de tous les affichages n'est pas encore appliquée.
- Les modifications du planning récurrent ne maintiennent pas une historisation complète des anciennes règles.
- Le rapport PDF passe par la fonction d'impression du navigateur.
- Les tests automatisés de rendu navigateur ont été bloqués par les restrictions d'exécution de l'environnement. Un test sur Chrome Android/Windows réel reste nécessaire.

## Contrôles réalisés
- Analyse syntaxique JavaScript (`node --check`) de l'application et du service worker.
- Tests unitaires Node : dates, calculs, état initial, récurrences, création et bilan de séances, génération ZIP compatible avec `.xlsx`.
- Validation ZIP par Python.
- Pas de test interactif Chrome réussi dans cet environnement : l'accès de Chrome aux URL de test a été bloqué.
