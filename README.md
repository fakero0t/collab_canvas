# CollabCanvas MVP

CollabCanvas is a real-time collaborative canvas application where multiple users can create, move, and interact with rectangles simultaneously. Users can pan and zoom the canvas, see each other's cursors in real-time, and work together on the same canvas with instant synchronization. The app handles authentication, manages user presence, and resolves conflicts when multiple users edit simultaneously. Built with Vue 3, Konva.js, and Firebase.

## Technology Stack

- **Frontend**: Vue 3 + Vite + TypeScript
- **Canvas**: Konva.js + Vue-Konva
- **Backend**: Firebase (Firestore + Auth + Hosting)
- **Styling**: CSS3 with custom components
- **Real-time**: Firestore real-time listeners

## Architecture Overview

```
┌─────────────────┐    ┌──────────────────┐    ┌─────────────────┐
│   Vue 3 App     │    │   Firestore      │    │  Firebase Auth  │
│                 │    │                  │    │                 │
│ • Canvas View   │◄──►│ • Rectangles     │    │ • Email/Pass    │
│ • Auth System   │    │ • Cursors        │    │ • Google OAuth  │
│ • Real-time UI  │    │ • Presence       │    │ • User Profiles │
└─────────────────┘    └──────────────────┘    └─────────────────┘
```

### Data Flow
1. **User Actions** → Local optimistic updates → Firestore persistence
2. **Firestore Changes** → Real-time listeners → UI updates across all clients
3. **Conflict Resolution** → Last write wins based on server timestamps

## Quick Start

### Prerequisites
- Node.js 18+ 
- npm or yarn
- Firebase account

### 1. Clone & Install
```bash
git clone <your-repo-url>
cd collab_canvas
cd ui
npm install
```

### 2. Firebase Setup
1. Create a new Firebase project at [console.firebase.google.com](https://console.firebase.google.com)
2. Enable Authentication (Email/Password + Google)
3. Create Firestore database
4. Get your Firebase config

### 3. Environment Configuration
Create `ui/.env.local`:
```env
VITE_FIREBASE_API_KEY=your_api_key
VITE_FIREBASE_AUTH_DOMAIN=your_project.firebaseapp.com
VITE_FIREBASE_PROJECT_ID=your_project_id
VITE_FIREBASE_STORAGE_BUCKET=your_project.appspot.com
VITE_FIREBASE_MESSAGING_SENDER_ID=your_sender_id
VITE_FIREBASE_APP_ID=your_app_id
```

### 4. Run Development Server
```bash
npm run dev
```

Visit `http://localhost:5173` and start collaborating!

## Deployment

### Build for Production
```bash
cd ui
npm run build
```

### Deploy to Firebase Hosting
```bash
# Install Firebase CLI (if not already installed)
npm install -g firebase-tools

# Login to Firebase
firebase login

# Deploy
firebase deploy
```

## Project Structure

```
collab_canvas/
├── ui/                          # Vue 3 frontend application
│   ├── src/
│   │   ├── components/          # Reusable Vue components
│   │   │   ├── Rectangle.vue    # Canvas rectangle component
│   │   │   ├── UserCursor.vue   # Multiplayer cursor display
│   │   │   ├── NavBar.vue       # Navigation and user info
│   │   │   ├── ErrorHandler.vue # Global error handling
│   │   │   └── ...
│   │   ├── composables/         # Vue composables (business logic)
│   │   │   ├── useAuth.js       # Authentication management
│   │   │   ├── useRectangles.js # Rectangle state management
│   │   │   ├── useCursors.js    # Cursor tracking
│   │   │   ├── usePresence.js   # User presence awareness
│   │   │   ├── useFirestore.js  # Firestore operations
│   │   │   └── ...
│   │   ├── views/               # Page components
│   │   │   ├── AuthView.vue     # Login/signup page
│   │   │   └── CanvasView.vue   # Main canvas workspace
│   │   └── utils/               # Utility functions
│   └── ...
├── firebase.json                # Firebase configuration
├── firestore.rules             # Firestore security rules
└── README.md                   # This file
```

## Development

### Key Composables

- **`useAuth`**: Handles authentication, user profiles, and sessions
- **`useRectangles`**: Manages rectangle state, creation, updates, and persistence  
- **`useFirestore`**: Abstracts Firestore operations with error handling and retries
- **`useCursors`**: Tracks real-time cursor positions with throttling
- **`usePresence`**: Manages user online/offline status and presence awareness
- **`usePerformance`**: Monitors and optimizes app performance
- **`useErrorHandling`**: Provides comprehensive error handling and recovery

---

Built with Vue 3, Konva.js, and Firebase
