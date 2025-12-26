# Gitesh's Simple Checklist

A brutally simple, high-end minimal checklist application with Firebase integration.

## Features

- Clean, minimal, classy UI
- Real-time sync across devices with Firebase Firestore
- Timestamp tracking for all entries
- Auto-linking for URLs
- Responsive design for mobile and desktop
- Dark mode support

## Setup Instructions

### 1. Create a Firebase Project

1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Click "Add project"
3. Enter project name: `gitesh-simple-checklist` (or your preferred name)
4. Follow the setup wizard

### 2. Enable Firestore Database

1. In your Firebase project, go to **Build** > **Firestore Database**
2. Click "Create database"
3. Start in **production mode** (we'll update rules)
4. Choose your preferred region
5. Click "Enable"

### 3. Get Firebase Configuration

1. Go to **Project Settings** (gear icon)
2. Scroll down to "Your apps"
3. Click the web icon `</>`
4. Register your app with a nickname
5. Copy the `firebaseConfig` object

### 4. Update Configuration

Edit `index.html` and replace the Firebase configuration (around line 411):

```javascript
const firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    authDomain: "YOUR_PROJECT_ID.firebaseapp.com",
    projectId: "YOUR_PROJECT_ID",
    storageBucket: "YOUR_PROJECT_ID.appspot.com",
    messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
    appId: "YOUR_APP_ID"
};
```

### 5. Install Firebase CLI

```bash
npm install -g firebase-tools
```

### 6. Login to Firebase

```bash
firebase login
```

### 7. Initialize Firebase in Your Project

```bash
cd gitesh-simple-checklist
firebase init
```

- Select **Firestore** and **Hosting**
- Choose "Use an existing project" and select your project
- Accept default Firestore rules file: `firestore.rules`
- Accept default Firestore indexes file
- For hosting:
  - Public directory: `.` (current directory)
  - Single-page app: `Yes`
  - Don't overwrite `index.html`

### 8. Deploy Firestore Rules

The `firestore.rules` file is already configured. Deploy it:

```bash
firebase deploy --only firestore:rules
```

### 9. Deploy to Firebase Hosting

```bash
firebase deploy --only hosting
```

Your app will be live at: `https://YOUR_PROJECT_ID.firebaseapp.com`

## Local Development

To test locally before deploying:

```bash
firebase serve
```

Visit `http://localhost:5000`

## Firestore Structure

The app uses a simple collection structure:

```
entries (collection)
  └── {auto-generated-id} (document)
      ├── text: string
      ├── timestamp: string (ISO format)
      └── completed: boolean
```

## Security Notes

The current Firestore rules allow anyone to read/write. For production use with authentication, update `firestore.rules`:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /entries/{entryId} {
      allow read, write: if request.auth != null;
    }
  }
}
```

## Deployment

After making changes:

```bash
git add .
git commit -m "Your commit message"
git push origin master
firebase deploy
```

## Tech Stack

- Vanilla JavaScript
- Firebase Firestore (Database)
- Firebase Hosting
- Responsive CSS with dark mode support
