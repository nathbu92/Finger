# Dice Finger — Build APK via GitHub Actions

## Comment ça marche

Le workflow `.github/workflows/build-apk.yml` se déclenche automatiquement à
chaque `push` sur `main` (ou manuellement via l'onglet **Actions** → **Run workflow**).

Il fait, dans une VM Ubuntu gratuite fournie par GitHub :
1. Installe Node.js + JDK 17 + Android SDK
2. `npm install` (Capacitor)
3. `npx cap add android` — génère le projet Android natif
4. `npx cap sync android` — copie `www/index.html` dans le projet
5. `./gradlew assembleDebug` — compile l'APK
6. Upload l'APK en tant qu'**artifact** téléchargeable

## Étapes pour toi

1. Crée un repo GitHub (public ou privé, peu importe)
2. Pousse tout le contenu de ce zip dedans :
   ```bash
   git init
   git add .
   git commit -m "Dice Finger"
   git remote add origin https://github.com/TON_USER/dice-finger.git
   git push -u origin main
   ```
3. Va dans l'onglet **Actions** du repo sur GitHub → le build se lance automatiquement
4. Une fois terminé (✅ vert), clique sur le run → en bas, section **Artifacts** →
   télécharge `dice-finger-debug-apk.zip`
5. Dézippe → tu obtiens `app-debug.apk`, installable directement sur Android

## Notes

- C'est un **APK debug**, non signé pour le Play Store mais installable direct
  sur un téléphone (active "Sources inconnues" dans les paramètres Android).
- Pour un APK release signé (prêt Play Store), il faudra ajouter une étape de
  signature avec un keystore stocké en **secret GitHub** — je peux l'ajouter
  si tu veux publier sur le Play Store.
- Aucune installation locale d'Android Studio nécessaire, tout tourne sur les
  serveurs GitHub gratuitement (2000 min/mois sur compte gratuit).
