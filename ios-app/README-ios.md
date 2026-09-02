# Anqā — app iOS native (usage personnel)

Ce dossier enveloppe la PWA `index.html` dans une vraie app iOS (via
[Capacitor](https://capacitorjs.com/)), installable directement sur ton
iPhone depuis Xcode. Les autres utilisateurs continuent d'utiliser la PWA
normalement (`add to home screen` depuis Safari) — rien ne change pour eux,
ce dossier ne touche pas à `index.html` à la racine du repo.

## Prérequis (sur le Mac)

- [Xcode](https://apps.apple.com/app/xcode/id497799835) installé depuis
  l'App Store (gratuit)
- [Node.js](https://nodejs.org/) (18+)
- [CocoaPods](https://cocoapods.org/) : `sudo gem install cocoapods`
- Ton iPhone connecté en USB (ou sur le même Wi-Fi pour un déploiement sans fil)
- Ton Apple ID personnel (compte gratuit suffit)

## Étapes

Depuis ce dossier (`ios-app/`) :

```bash
# 1. Installer les dépendances
npm install

# 2. Générer le projet Xcode iOS (une seule fois)
npx cap add ios

# 3. Générer les icônes et l'écran de démarrage à partir de resources/
npm run assets

# 4. Synchroniser le contenu web dans le projet natif
npm run sync

# 5. Ouvrir le projet dans Xcode
npm run open
```

Dans Xcode, une fois le projet ouvert :

1. Sélectionne le projet **App** dans le panneau de gauche → onglet
   **Signing & Capabilities**.
2. Dans **Team**, choisis ton Apple ID personnel (ajoute-le via
   *Xcode → Settings → Accounts* si besoin — un compte gratuit suffit).
3. Change le **Bundle Identifier** si `com.jambou.anqa` est déjà pris par
   quelqu'un d'autre (rare, mais Xcode te préviendra en rouge si besoin) —
   remplace `com.jambou` par autre chose d'unique, ex. `com.tonprenom.anqa`.
4. Branche ton iPhone en USB, sélectionne-le comme cible en haut de la
   fenêtre Xcode (à côté du bouton ▶️).
5. Clique sur ▶️ **Run**. Xcode compile, installe et lance l'app sur ton
   téléphone.
6. Première ouverture sur l'iPhone : va dans **Réglages → Général →
   VPN et gestion de l'appareil**, et fais confiance à ton Apple ID
   développeur. Relance l'app.

## Limite du compte gratuit

Avec un Apple ID gratuit (pas de compte développeur payant à 99 $/an),
l'app se réinstalle avec une validité de **7 jours** — passé ce délai, il
faut refaire l'étape 5 (rebrancher l'iPhone, relancer depuis Xcode) pour la
"re-signer". Avec un compte payant, plus besoin de repasser par là.

## Mettre à jour l'app plus tard

Si `index.html` change à la racine du repo, recopie-le dans
`ios-app/www/index.html`, puis relance `npm run sync` et réinstalle depuis
Xcode (étape 5).

## Ce que fait/ne fait pas cette app

- Vraie icône sur l'écran d'accueil, lancement en plein écran, comme une
  app native — pas de barre Safari.
- Utilise le même backend (Supabase, Open Food Facts, Withings) que la
  version web : connexion internet nécessaire, comme pour la PWA.
- N'est pas publiée sur l'App Store — c'est un build local, uniquement
  pour ton téléphone (ou ceux sur lesquels tu l'installes manuellement).
