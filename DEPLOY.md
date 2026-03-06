# OSINT Threat Suite — GitHub Pages Deployment

## File Structure
Your repo should look exactly like this:
```
osint-suite/
├── index.html
├── manifest.json
├── sw.js
└── icons/
    ├── icon-192.png
    └── icon-512.png
```

---

## Step-by-Step Deployment

### 1. Create a GitHub Account
Go to https://github.com and sign up (free).

### 2. Create a New Repository
- Click the green **"New"** button
- Name it: `osint-suite`
- Set to **Public** (required for free GitHub Pages)
- Do NOT initialize with README
- Click **Create repository**

### 3. Upload Your Files
Option A — GitHub Web UI (easiest, no Git needed):
- On your new repo page, click **"uploading an existing file"**
- Drag and drop ALL files: `index.html`, `manifest.json`, `sw.js`
- Click **Commit changes**
- Then click **"Create new file"**, name it `icons/icon-192.png`
  - Click the upload area and upload icon-192.png
  - Repeat for `icons/icon-512.png`

Option B — Git command line:
```bash
git init
git add .
git commit -m "Initial OTS deployment"
git branch -M main
git remote add origin https://github.com/YOURUSERNAME/osint-suite.git
git push -u origin main
```

### 4. Enable GitHub Pages
- Go to your repo → **Settings** tab
- Left sidebar → **Pages**
- Under "Source" → select **Deploy from a branch**
- Branch: **main** / folder: **/ (root)**
- Click **Save**
- Wait ~60 seconds → your URL will appear:
  `https://YOURUSERNAME.github.io/osint-suite`

---

## ⚠️ Important: Fix the manifest start_url

Because GitHub Pages serves from a subdirectory path, open `manifest.json`
and change this line:

```json
"start_url": "/"
```

to:

```json
"start_url": "/osint-suite/"
```

And in `sw.js`, update the ASSETS array root:
```js
'/',  →  '/osint-suite/',
'/index.html',  →  '/osint-suite/index.html',
```

---

## Install as PWA on iPhone

1. Open your GitHub Pages URL in **Safari** (not Chrome)
2. Tap the **Share icon** (box with upward arrow) at the bottom
3. Tap **"Add to Home Screen"**
4. Rename to **"OTS"** or **"OSINT Suite"**
5. Tap **Add**

The app now launches fullscreen from your home screen with no browser UI.

---

## Install on Android

1. Open the URL in Chrome
2. Tap the three-dot menu → **"Add to Home Screen"** or
   Chrome may auto-prompt with an install banner
3. Tap **Install**

---

## Updating the App

Any time you push changes to GitHub, the site updates automatically
within a few minutes. Users will get the new version on next load
(service worker handles cache refresh).
