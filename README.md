# KeyPlayers HQ — VA Onboarding Handbook

A web-based onboarding handbook with built-in acknowledgment tracking.

## Project Structure

```
keyplayers-handbook/
├── index.html              # The handbook (single HTML file)
├── images/                 # Team member photos
│   ├── mitch-conquer.png
│   ├── olivia-greenberg.png
│   └── ... (18 total)
├── google-apps-script.gs   # Backend for Google Sheets tracking
└── README.md
```

---

## Deployment Guide

### Step 1: Set Up Google Apps Script Backend

1. Open **Google Sheets** and create a new blank spreadsheet
2. Name it `KeyPlayers Handbook Tracker`
3. Go to **Extensions > Apps Script**
4. Delete any existing code in `Code.gs`
5. Copy the entire contents of `google-apps-script.gs` and paste it in
6. Click **Run > setupSheet** to create the headers (authorize when prompted)
7. Click **Deploy > New deployment**
8. Click the gear icon, select **Web app**
9. Set:
   - **Description:** `Handbook Tracker v1`
   - **Execute as:** `Me`
   - **Who has access:** `Anyone`
10. Click **Deploy** and **Authorize access**
11. Copy the **Web App URL** — you'll need this next

### Step 2: Connect the HTML to Your Backend

1. Open `index.html`
2. Find this line near the bottom:
   ```javascript
   const SCRIPT_URL = 'YOUR_GOOGLE_APPS_SCRIPT_URL_HERE';
   ```
3. Replace `YOUR_GOOGLE_APPS_SCRIPT_URL_HERE` with your Web App URL from Step 1

### Step 3: Push to GitHub

```bash
# Initialize the repo
cd keyplayers-handbook
git init
git add .
git commit -m "Initial commit: KeyPlayers VA Handbook"

# Create repo on GitHub, then:
git remote add origin https://github.com/YOUR_USERNAME/keyplayers-handbook.git
git branch -M main
git push -u origin main
```

### Step 4: Deploy to Vercel

1. Go to [vercel.com](https://vercel.com) and sign in with GitHub
2. Click **Add New > Project**
3. Import your `keyplayers-handbook` repository
4. Framework preset: **Other**
5. Click **Deploy**
6. Your handbook is now live at `https://keyplayers-handbook.vercel.app` (or your custom domain)

### Optional: Custom Domain

In Vercel dashboard:
1. Go to your project **Settings > Domains**
2. Add your custom domain (e.g., `handbook.keyplayershq.com`)
3. Follow the DNS instructions provided

---

## What Gets Tracked

When a VA submits the acknowledgment form, the Google Sheet logs:

| Column | Description |
|--------|-------------|
| Timestamp | ISO timestamp of submission |
| Full Name | VA's full name |
| Email | VA's email address |
| Employee ID | Optional ID |
| Position | VA's role |
| Client Assigned | Which client they work with |
| Date Signed | Human-readable date |
| Sections Confirmed | Which sections they checked |
| Signature Link | Google Drive link to signature image |
| Status | "Acknowledged" |

An email notification is also sent to `training@keyplayershq.com` for each submission.

---

## Features

- **Accordion sections** — clean, scannable layout
- **Read enforcement** — form stays locked until all 13 sections are opened
- **Progress bar** — sticky top bar shows reading progress
- **Digital signature pad** — canvas-based, works on mobile
- **Google Sheets backend** — automatic logging with formatted headers
- **Email notifications** — HR gets notified on each submission
- **Signature storage** — saved as PNG in Google Drive with shareable links
- **Responsive design** — works on desktop, tablet, and mobile
