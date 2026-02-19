# GRE Quant 170 — Setup Guide

## Quick Deploy to GitHub Pages

1. Create a new GitHub repository (e.g., `gre-quant-170`)
2. Upload `index.html` to the repository root
3. Go to **Settings → Pages → Source → Deploy from branch → main → / (root)**
4. Your app is live at `https://yourusername.github.io/gre-quant-170/`

The app works immediately with localStorage (offline progress saving).

---

## Enable Google Sign-In + Cloud Sync (Optional)

### Step 1: Create Firebase Project
1. Go to [Firebase Console](https://console.firebase.google.com)
2. Click **"Add project"** → name it (e.g., "GRE Quant 170")
3. Disable Google Analytics (optional) → Create

### Step 2: Enable Google Authentication
1. In Firebase Console → **Authentication → Get Started**
2. Click **Sign-in method → Google → Enable**
3. Set a support email → **Save**
4. Go to **Settings → Authorized domains**
5. Add your GitHub Pages domain: `yourusername.github.io`

### Step 3: Enable Firestore
1. Go to **Firestore Database → Create database**
2. Select **"Start in test mode"** (for development)
3. Choose a region → **Enable**

### Step 4: Get Your Config
1. Go to **Project Settings** (gear icon) → **Your apps** → **Web** (</> icon)
2. Register app (any name) → Copy the `firebaseConfig` object
3. Open `index.html` and replace the `FIREBASE_CONFIG` section:

```javascript
const FIREBASE_CONFIG = {
  apiKey: "AIzaSy...",           // Your actual key
  authDomain: "your-project.firebaseapp.com",
  projectId: "your-project-id",
  storageBucket: "your-project.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123:web:abc..."
};
```

4. Commit and push. Google Sign-In is now live!

### Step 5: Secure Firestore (Production)
Replace Firestore rules with:
```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{userId} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
    }
  }
}
```

---

## Features
- **1000+ procedurally generated questions** across all 5 GRE Quant topics
- **10 concept sub-categories per topic** (50 total)
- **3 difficulty levels** (Easy, Medium, Hard)
- **Chart questions** (bar, pie, line charts)
- **Mental Math Gym** with 9 operation types × 4 difficulty levels
- **40+ shortcut techniques** organized by topic
- **Dashboard** with predicted score, accuracy trends, per-topic correct/incorrect
- **Google Sign-In** for cross-device cloud sync
- **Dark/Light theme** toggle
- **GitHub Pages compatible** (100% static, client-side)
