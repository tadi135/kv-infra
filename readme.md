# KV Infra & Interiors — Website

> Professional construction & interior design website with Firebase backend and hidden admin panel.

**Live site:** `https://YOUR-USERNAME.github.io/kv-infra-website/`
**Admin panel:** `https://YOUR-USERNAME.github.io/kv-infra-website/admin.html`

---

## 📁 Project Structure

```
kv-infra-website/
├── index.html      ← Public website (customers see this)
├── admin.html      ← Hidden admin panel (you only)
└── README.md
```

---

## 🔥 Step 1 — Firebase Setup

### 1.1 Create a Firebase Project
1. Go to **https://console.firebase.google.com**
2. Click **Add project** → Enter name (e.g. `kv-infra`) → Create project

### 1.2 Enable Firestore Database
1. Build → **Firestore Database** → Create database
2. Choose **Start in test mode** → Region: **asia-south1 (Mumbai)** → Done

### 1.3 Enable Authentication
1. Build → **Authentication** → Get Started
2. Sign-in method → **Email/Password** → Enable → Save

### 1.4 Create Your Admin User
1. Authentication → **Users tab** → **Add user**
2. Enter your admin email + strong password → Add user

### 1.5 Get Your Firebase Config
1. Project Settings (⚙) → Your apps → Web (`</>`) → Register app
2. Copy the `firebaseConfig` object shown

### 1.6 Paste Config Into Both Files
Open `index.html` AND `admin.html`, find `firebaseConfig` near the top, replace all `"YOUR_..."` values with your actual config.

### 1.7 Set Firestore Security Rules
Firestore Database → Rules → paste the following → Publish:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /leads/{doc} {
      allow create: if true;
      allow read, delete: if request.auth != null;
    }
    match /reviews/{doc} {
      allow read: if true;
      allow write, delete: if request.auth != null;
    }
  }
}
```

---

## 🐙 Step 2 — GitHub Setup & Hosting

### 2.1 Create a GitHub Repository
1. Go to **github.com** → New repository
2. Name: `kv-infra-website` → Public → Create repository

### 2.2 Upload Files
Repo page → **Add file → Upload files** → drag `index.html`, `admin.html`, `README.md` → Commit changes

OR via Git:
```bash
git init
git add .
git commit -m "KV Infra website"
git remote add origin https://github.com/YOUR-USERNAME/kv-infra-website.git
git push -u origin main
```

### 2.3 Enable GitHub Pages
Repo → **Settings** → **Pages** → Source: **main / (root)** → Save

Your site goes live at:
```
https://YOUR-USERNAME.github.io/kv-infra-website/
```
Admin panel at:
```
https://YOUR-USERNAME.github.io/kv-infra-website/admin.html
```
**Keep the admin URL private — it is not linked from the public site.**

---

## 📱 How It Works

| Feature | How |
|---|---|
| Contact form | Saves to Firestore `leads` + opens WhatsApp with customer details |
| Admin login | Firebase Email/Password Auth |
| View leads | Admin → Contact Leads tab — WhatsApp reply button per lead |
| Add reviews | Admin → Add Review → live on website immediately |
| Reviews display | Read from Firestore `reviews` collection |
| Fallback | localStorage if Firebase not yet configured |

---

## ✅ Quick Checklist

- [ ] Firebase project created
- [ ] Firestore enabled (asia-south1)
- [ ] Auth enabled (Email/Password)
- [ ] Admin user created in Firebase Auth
- [ ] firebaseConfig pasted in index.html AND admin.html
- [ ] Firestore security rules published
- [ ] Files uploaded to GitHub
- [ ] GitHub Pages enabled
- [ ] Site live and tested
- [ ] Admin URL saved privately
