# GitHub Pages Setup Guide

Follow these steps to host your Command Center Pro on GitHub Pages.

## 📋 Prerequisites

- A GitHub account (free) - Sign up at https://github.com/signup if you don't have one

## 🚀 Deployment Steps

### Step 1: Create GitHub Repository

1. Go to https://github.com
2. Click the **"+"** icon in top right → **"New repository"**
3. Fill in:
   - **Repository name**: `command-center` (or any name you like)
   - **Description**: "Personal Command Center - Life Management App"
   - **Public** or **Private** (both work with GitHub Pages)
   - ✅ Check "Add a README file" (optional, we have our own)
4. Click **"Create repository"**

### Step 2: Upload Files

**Method A: Using GitHub Web Interface (Easiest)**

1. In your new repository, click **"Add file"** → **"Upload files"**
2. Drag and drop these files:
   - `index.html` (the main app file)
   - `README.md` (the documentation)
3. Scroll down, add commit message: "Initial commit"
4. Click **"Commit changes"**

**Method B: Using Git Command Line**

```bash
# Clone your repository
git clone https://github.com/YOUR-USERNAME/command-center.git
cd command-center

# Copy files into the directory
# (copy index.html and README.md here)

# Commit and push
git add .
git commit -m "Initial commit"
git push origin main
```

### Step 3: Enable GitHub Pages

1. In your repository, click **"Settings"** (top menu)
2. Scroll down and click **"Pages"** in the left sidebar
3. Under "Branch", select:
   - Branch: **main** (or master)
   - Folder: **/ (root)**
4. Click **"Save"**
5. Wait 1-2 minutes for deployment

### Step 4: Access Your App!

Your app will be live at:
```
https://YOUR-USERNAME.github.io/command-center/
```

For example, if your GitHub username is "john-doe":
```
https://john-doe.github.io/command-center/
```

## 🎉 You're Done!

- Bookmark the URL for easy access
- Share it with anyone (if repo is public)
- Access from any device with internet
- Your data stays private in your browser

## 📱 Bonus: Add to Phone Home Screen

### iPhone/iPad:
1. Open the URL in Safari
2. Tap the Share button
3. Scroll down and tap "Add to Home Screen"
4. Name it "Command Center"
5. Tap "Add"

### Android:
1. Open the URL in Chrome
2. Tap the three dots menu
3. Tap "Add to Home Screen"
4. Name it "Command Center"
5. Tap "Add"

Now it works like a native app!

## 🔄 Updating Your App

When you want to update:

1. Go to your repository on GitHub
2. Click on `index.html`
3. Click the pencil icon (Edit)
4. Make changes
5. Scroll down and click "Commit changes"
6. Wait 1-2 minutes for redeployment

## 🆘 Troubleshooting

**"404 - Not Found" error:**
- Wait 2-3 minutes after enabling Pages
- Check that you selected the correct branch
- Verify the file is named `index.html` (not `index.html.html`)

**"Changes not showing up":**
- Clear browser cache (Ctrl+Shift+Delete)
- Hard refresh (Ctrl+Shift+R or Cmd+Shift+R)
- Wait a few minutes for GitHub to update

**"App not working":**
- Open browser console (F12) to check for errors
- Make sure you're using a modern browser
- Try in incognito/private mode

## 💡 Tips

- **Custom Domain**: You can use your own domain name (e.g., mycenter.com) - see GitHub Pages docs
- **HTTPS**: GitHub Pages automatically provides SSL/HTTPS
- **Analytics**: Add Google Analytics if you want to track usage
- **Updates**: Any push to the main branch automatically updates the live site

## 🔐 Privacy Note

Even though your app is hosted on GitHub:
- Your personal data (events, tasks, ideas) is stored ONLY in your browser's localStorage
- Nothing is sent to GitHub or any server
- Each user has their own isolated data
- Clearing browser data will delete your info (export regularly!)

---

Need help? Check GitHub's official Pages documentation: https://docs.github.com/en/pages
