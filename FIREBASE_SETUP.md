# Firebase Setup Guide for Personal Kanban

This guide will help you set up Firebase to enable Google account sync for the Personal Kanban app.

## Prerequisites
- A Google account
- Access to [Firebase Console](https://console.firebase.google.com/)

## Step 1: Create a Firebase Project

1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Click **"Add project"** or **"Create a project"**
3. Enter a project name (e.g., "personal-kanban")
4. Accept the terms and click **Continue**
5. Disable Google Analytics (optional, not needed for this app)
6. Click **Create project**

## Step 2: Set Up Authentication

1. In your Firebase project, click **"Authentication"** in the left sidebar
2. Click **"Get started"**
3. Click on **"Google"** under Sign-in providers
4. Toggle **"Enable"**
5. Select a support email (your email)
6. Click **"Save"**

## Step 3: Set Up Firestore Database

1. Click **"Firestore Database"** in the left sidebar
2. Click **"Create database"**
3. Choose **"Start in production mode"** (we'll add rules next)
4. Choose a location (select one closest to your users)
5. Click **"Enable"**

## Step 4: Configure Firestore Security Rules

1. In Firestore Database, click on the **"Rules"** tab
2. Replace the default rules with:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // Users can only read/write their own kanban board
    match /kanban_boards/{userId} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
    }
  }
}
```

3. Click **"Publish"**

## Step 5: Get Your Firebase Config

1. Go to **Project Settings** (gear icon in left sidebar)
2. Scroll down to **"Your apps"**
3. Click the **Web icon** (`</>`) to add a web app
4. Give your app a nickname (e.g., "kanban-web")
5. Click **"Register app"**
6. Copy the `firebaseConfig` object
7. Open `index.html` and find this section (around line 170):

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

8. Replace with your actual Firebase config values

## Step 6: Add Authorized Domain

1. In Firebase Console, go to **Authentication** > **Settings** tab
2. Scroll to **Authorized domains**
3. Add your domain (e.g., `ralvid.github.io`)
4. Click **Add domain**

## Step 7: Test the App

1. Open your app in a browser
2. You should see a **"🔐 Logga in"** button
3. Click it to sign in with Google
4. After signing in, your tasks will sync to Firebase
5. Open the app on another browser/device and sign in with the same Google account
6. Your tasks should sync automatically!

## Features

✅ **Google Sign-In** - One-click authentication
✅ **Real-time Sync** - Changes sync across all your devices instantly
✅ **Offline Support** - Works offline, syncs when back online
✅ **Private Data** - Each user's data is isolated and secure
✅ **Sync Indicator** - Visual feedback showing sync status

## Troubleshooting

### "Firebase not configured properly"
- Check that you've replaced all placeholder values in `firebaseConfig`
- Ensure the config values are correct (copy-paste from Firebase Console)

### Authentication popup blocked
- Check your browser's popup blocker settings
- Allow popups for your domain

### "Permission denied" errors
- Verify Firestore security rules are set correctly
- Ensure you're signed in with a Google account

### Sync not working
- Check browser console for errors
- Verify you have internet connection
- Try signing out and signing back in

## Cost

Firebase offers a generous free tier:
- **Firestore**: 50K reads/day, 20K writes/day, 1GB storage
- **Authentication**: Unlimited users

For personal use, you'll likely stay within the free tier limits.

## Privacy & Security

- All data is stored in your personal Google account
- Each user can only access their own data
- Firebase uses industry-standard encryption
- You can delete your data anytime by going to Firebase Console > Firestore Database

## Support

If you need help:
1. Check Firebase documentation: https://firebase.google.com/docs
2. Review the troubleshooting section above
3. Check browser console for error messages
