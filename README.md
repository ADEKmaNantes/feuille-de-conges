# Fiche Congés / Absences — ADEKMA

Formulaire HTML permettant à un salarié de remplir une demande de congés
payés / absences, de signer sur l'écran, puis de générer le PDF officiel
ADEKMA rempli et de l'envoyer directement à l'exploitation concernée
(Manutention ou Levage). L'application est **installable** (PWA) une fois
déployée en HTTPS.

## Fichiers du dépôt

- `index.html` — la page de l'application (formulaire + logique PDF).
- `manifest.json` — décrit l'application (nom, icônes, couleurs) pour permettre
  son installation depuis le navigateur.
- `sw.js` — service worker minimal : condition technique nécessaire (avec le
  manifest) pour que le navigateur propose l'installation, et permet un accès
  hors-ligne une fois l'application ouverte une première fois.
- `icon-192.png`, `icon-512.png`, `apple-touch-icon.png` — icônes de
  l'application (fond jaune ADEKMA).

**Tous ces fichiers doivent être poussés ensemble et rester à la racine du
site** (ne pas renommer `index.html`, ni déplacer les icônes/manifest/sw.js
dans un sous-dossier, sauf à adapter les chemins dans `index.html` et
`manifest.json` en conséquence).

## Fonctionnement

- Le PDF officiel ADEKMA est intégré tel quel dans la page (en base64) et sert
  de modèle : les données saisies sont superposées dessus via la librairie
  [pdf-lib](https://pdf-lib.js.org/) (chargée depuis un CDN), donc le rendu est
  strictement identique au document papier d'origine.
- Aucun serveur ni backend : tout se passe dans le navigateur.
- Bouton **Envoyer** : sur mobile, ouvre le partage natif avec le PDF en pièce
  jointe ; sur desktop, télécharge le PDF puis ouvre un e-mail pré-rempli.
- Bouton **Télécharger le PDF** : génère et télécharge le PDF sans passer par
  l'envoi.
- Bouton **Prévisualiser la fiche** : affiche un aperçu du PDF généré dans une
  fenêtre, via pdf.js (CDN).
- Les données saisies (champs + signature) sont sauvegardées automatiquement
  dans le navigateur et restaurées à la prochaine ouverture ; seule une
  réinitialisation volontaire (menu du logo) les efface.

## Installation de l'application (PWA)

Une fois le site déployé en HTTPS (GitHub Pages convient), les visiteurs
peuvent installer l'application :
- **Android / Chrome / Edge** : une option « Installer l'application » apparaît
  automatiquement dans le menu du logo (☰) de la page, ou via le menu du
  navigateur (⋮ → "Installer l'application" / "Ajouter à l'écran d'accueil").
- **iOS / Safari** : menu Partager → « Sur l'écran d'accueil » (pas de bannière
  automatique, c'est une limitation d'iOS).

⚠️ L'installation ne fonctionne **que** sur la version hébergée en HTTPS —
un fichier `index.html` ouvert seul en local (`file://`) ne peut pas être
installé, c'est une restriction de sécurité des navigateurs (le service worker
et le manifest ne se chargent pas sur `file://`).

## Mise en ligne sur GitHub Pages

1. Créer un nouveau dépôt (par ex. `feuille-de-conges`) sur le compte/organisation
   GitHub utilisé pour les autres formulaires ADEKMA (`adekmanantes`).
2. Depuis ce dossier :

   ```bash
   git init
   git add .
   git commit -m "Fiche congés / absences ADEKMA (PWA installable)"
   git branch -M main
   git remote add origin https://github.com/adekmanantes/feuille-de-conges.git
   git push -u origin main
   ```

3. Sur GitHub : **Settings → Pages → Source : branche `main`, dossier `/ (root)`**,
   puis Enregistrer.
4. La page sera disponible à l'adresse :
   `https://adekmanantes.github.io/feuille-de-conges/`

## Intégration à la page d'accueil

Une fois en ligne, ajouter un lien vers cette URL dans la page d'accueil des
formulaires (`page_d-accueil_adekma`), à côté des autres fiches (feuille
d'heures, garage, prêt/emprunt de matériel).

## Mise à jour

Toute modification se fait en éditant les fichiers puis en re-poussant sur
GitHub (`git add`, `git commit`, `git push`) — GitHub Pages se met à jour
automatiquement en quelques dizaines de secondes. Le numéro de version affiché
dans l'application (constante `APP_VERSION` dans `index.html`) est à
incrémenter à chaque mise à jour.
