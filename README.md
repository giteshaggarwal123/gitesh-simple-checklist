# Gitesh's Simple Checklist

A brutally simple, high-end minimal checklist application with Firebase integration.

## Features

- Clean, minimal, classy UI
- Real-time sync across devices with Firebase Firestore
- **File attachments**: Attach any file type or paste images directly (via Cloudinary - FREE)
- Timestamp tracking for all entries
- Auto-linking for URLs
- Responsive design for mobile and desktop
- Dark mode support
- 25GB free storage with Cloudinary CDN

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

### 3. Enable Firebase Storage

1. In your Firebase project, go to **Build** > **Storage**
2. Click "Get started"
3. Start in **production mode** (we'll update rules)
4. Choose the same region as Firestore
5. Click "Done"

### 4. Get Firebase Configuration

1. Go to **Project Settings** (gear icon)
2. Scroll down to "Your apps"
3. Click the web icon `</>`
4. Register your app with a nickname
5. Copy the `firebaseConfig` object

### 5. Update Configuration

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

### 6. Install Firebase CLI

```bash
npm install -g firebase-tools
```

### 7. Login to Firebase

```bash
firebase login
```

### 8. Initialize Firebase in Your Project

```bash
cd gitesh-simple-checklist
firebase init
```

- Select **Firestore**, **Storage**, and **Hosting**
- Choose "Use an existing project" and select your project
- Accept default Firestore rules file: `firestore.rules`
- Accept default Firestore indexes file
- Accept default Storage rules file: `storage.rules`
- For hosting:
  - Public directory: `.` (current directory)
  - Single-page app: `Yes`
  - Don't overwrite `index.html`

### 9. Deploy Rules

The `firestore.rules` and `storage.rules` files are already configured. Deploy them:

```bash
firebase deploy --only firestore:rules,storage:rules
```

### 10. Deploy to Firebase Hosting

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

## Usage

### Adding Entries

1. Type your task, goal, or note in the text field
2. **Attach files** by clicking "Attach File" button
3. **Paste images** directly using Ctrl+V (Cmd+V on Mac)
4. Press Enter or click "Add" to save

### Attachments

- **Supported**: All file types (images, PDFs, documents, etc.)
- **Images**: Display inline with preview
- **Other files**: Show as downloadable links
- **Limit**: 10MB per file

### Managing Entries

- Click "Done" to mark as complete
- Click "Undo" to revert completion
- Click "Delete" to remove entry
- Click on images to open full size

## Data Structure

### Firestore

The app uses a simple collection structure:

```
entries (collection)
  └── {auto-generated-id} (document)
      ├── text: string
      ├── timestamp: string (ISO format)
      ├── completed: boolean
      └── attachments: array (optional)
          └── [
              {
                name: string,
                url: string,
                type: string,
                size: number
              }
            ]
```

### Storage

Files are stored in Firebase Storage under the `attachments/` directory:

```
attachments/
  └── {timestamp}_{filename}
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
