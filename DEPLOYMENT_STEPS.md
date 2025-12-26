# Firebase Deployment Steps

Your Firebase configuration has been added to the code. Follow these steps to complete the deployment:

## Step 1: Login to Firebase

Open a new terminal/command prompt and run:

```bash
cd C:\Users\gites\gitesh-simple-checklist
firebase login
```

This will open your browser for authentication. Login with: **gitesh.aggarwal489@gmail.com**

## Step 2: Initialize Firebase Project

```bash
firebase init
```

When prompted:
- **Which Firebase features?** Select:
  - [x] Firestore
  - [x] Storage
  - [x] Hosting

  Use spacebar to select, Enter to confirm

- **Select a default Firebase project:** Choose `gitesh-simple`

- **Firestore Rules file:** Press Enter (use default: `firestore.rules`)
  - **File firestore.rules already exists. Overwrite?** → **No**

- **Firestore indexes file:** Press Enter (use default)

- **Storage Rules file:** Press Enter (use default: `storage.rules`)
  - **File storage.rules already exists. Overwrite?** → **No**

- **Public directory:** Type `.` and press Enter

- **Configure as single-page app?** → **Yes**

- **File index.html already exists. Overwrite?** → **No**

- **Set up automatic builds?** → **No**

## Step 3: Deploy Firestore Rules

```bash
firebase deploy --only firestore:rules
```

This uploads the database security rules.

## Step 4: Deploy Storage Rules

```bash
firebase deploy --only storage:rules
```

This uploads the file storage security rules.

## Step 5: Deploy Your App

```bash
firebase deploy --only hosting
```

This uploads your app to Firebase Hosting.

## Step 6: Access Your App

After deployment completes, you'll see:

```
✔  Deploy complete!

Hosting URL: https://gitesh-simple.web.app
```

Your app will be live at:
- **https://gitesh-simple.web.app**
- **https://gitesh-simple.firebaseapp.com**

## Troubleshooting

### If you get "Permission denied" errors:
```bash
firebase deploy --only firestore:rules,storage:rules,hosting
```

### To test locally before deploying:
```bash
firebase serve
```
Then visit: http://localhost:5000

### To view deployment logs:
```bash
firebase deploy --debug
```

## Quick Deploy (After First Setup)

For future updates:
```bash
git add .
git commit -m "Your update message"
git push origin master
firebase deploy
```

This deploys everything at once.
