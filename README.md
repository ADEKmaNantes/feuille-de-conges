# Fiche Congés / Absences — ADEKMA Ouest

Formulaire HTML autonome (une seule page, `index.html`) permettant à un salarié de
remplir une demande de congés payés / absences, de signer sur l'écran, puis de
générer le PDF officiel ADEKMA Ouest rempli et de l'envoyer directement à
l'exploitation concernée (Manutention ou Levage).

## Fonctionnement

- Le PDF officiel ADEKMA Ouest est intégré tel quel dans la page (en base64) et
  sert de modèle : les données saisies sont superposées dessus via la librairie
  [pdf-lib](https://pdf-lib.js.org/) (chargée depuis un CDN), donc le rendu est
  strictement identique au document papier d'origine.
- Aucune dépendance à installer, aucun serveur ni backend : tout se passe dans le
  navigateur. Il suffit d'héberger le fichier `index.html`.
- Bouton **Envoyer** : sur mobile, ouvre le partage natif avec le PDF en pièce
  jointe ; sur desktop, télécharge le PDF puis ouvre un e-mail pré-rempli.
- Bouton **Télécharger le PDF** : génère et télécharge le PDF sans passer par
  l'envoi.

## Mise en ligne sur GitHub Pages

1. Créer un nouveau dépôt (par ex. `Fiche-Conges-Absences`) sur le compte/organisation
   GitHub utilisé pour les autres formulaires ADEKMA (`adekmanantes`).
2. Depuis ce dossier :

   ```bash
   git init
   git add index.html README.md
   git commit -m "Fiche congés / absences ADEKMA Ouest"
   git branch -M main
   git remote add origin https://github.com/adekmanantes/Fiche-Conges-Absences.git
   git push -u origin main
   ```

3. Sur GitHub : **Settings → Pages → Source : branche `main`, dossier `/ (root)`**,
   puis Enregistrer.
4. La page sera disponible à l'adresse :
   `https://adekmanantes.github.io/Fiche-Conges-Absences/`

## Intégration à la page d'accueil

Une fois en ligne, ajouter un lien vers cette URL dans la page d'accueil des
formulaires (`page_d-accueil_adekma`), à côté des autres fiches (feuille
d'heures, garage, prêt/emprunt de matériel).

## Mise à jour

Toute modification se fait simplement en éditant `index.html` puis en
re-poussant sur GitHub (`git add`, `git commit`, `git push`) — GitHub Pages se
met à jour automatiquement en quelques dizaines de secondes.
