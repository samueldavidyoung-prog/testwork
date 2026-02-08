# Railway Deployment Guide - Road Surfacing Tracker

## 📦 Files You Need

Make sure you have ALL these files in your project folder:

```
RoadTracker/
├── server.js
├── road-surfacing-tracker-realtime.html
├── package.json
├── railway.json          ← NEW
├── Procfile              ← NEW
├── .gitignore            ← NEW
└── README.md
```

---

## 🚀 Step-by-Step Railway Deployment

### **Step 1: Install Git (if you haven't already)**

**Windows:**
1. Download from https://git-scm.com/download/win
2. Run installer with default options
3. Restart your terminal/command prompt

**Mac:**
```bash
# Install Homebrew first (if not installed)
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Then install git
brew install git
```

**Linux:**
```bash
sudo apt install git -y
```

Verify installation:
```bash
git --version
```

---

### **Step 2: Create a GitHub Account and Repository**

1. Go to https://github.com/signup
2. Create a free account
3. Verify your email
4. Click the "+" icon (top right) → "New repository"
5. Repository name: `road-tracker`
6. Keep it **Public**
7. Do NOT check "Add a README"
8. Click "Create repository"

**Keep this page open** - you'll need the URL!

---

### **Step 3: Push Your Code to GitHub**

Open terminal/command prompt in your `RoadTracker` folder:

**Windows (Command Prompt):**
```bash
cd C:\Users\YourName\RoadTracker
```

**Mac/Linux (Terminal):**
```bash
cd ~/RoadTracker
```

Now run these commands **one by one**:

```bash
# Initialize git
git init

# Add all files
git add .

# Commit files
git commit -m "Initial commit"

# Add your GitHub repository (REPLACE with your actual URL!)
git remote add origin https://github.com/YOUR-USERNAME/road-tracker.git

# Rename branch to main
git branch -M main

# Push to GitHub
git push -u origin main
```

**If asked for credentials:**
- Username: Your GitHub username
- Password: You need a **Personal Access Token** (not your password!)
  - Go to: https://github.com/settings/tokens
  - Click "Generate new token (classic)"
  - Check "repo" checkbox
  - Click "Generate token"
  - Copy the token and use it as password

---

### **Step 4: Deploy to Railway**

1. Go to https://railway.app
2. Click "Login" → Choose "Login with GitHub"
3. Authorize Railway
4. Click "New Project"
5. Select "Deploy from GitHub repo"
6. Choose your `road-tracker` repository
7. Railway will automatically detect it's a Node.js app

**Wait for deployment** (usually 2-3 minutes)

---

### **Step 5: Get Your Public URL**

1. In Railway, click on your deployed service
2. Go to "Settings" tab
3. Scroll to "Domains" section
4. Click "Generate Domain"
5. You'll get something like: `road-tracker-production.up.railway.app`

**Copy this URL!**

---

### **Step 6: Update Your Frontend**

You need to update the HTML file to use your new Railway URL.

Open `road-surfacing-tracker-realtime.html` and find this line (around line 267):

```javascript
const API_URL = 'http://localhost:3000/api';
```

Change it to:
```javascript
const API_URL = 'https://road-tracker-production.up.railway.app/api';
```

**Replace with YOUR actual Railway domain!**

Save the file.

---

### **Step 7: Upload the Updated HTML to GitHub**

```bash
# Add the changed file
git add road-surfacing-tracker-realtime.html

# Commit the change
git commit -m "Update API URL for Railway"

# Push to GitHub
git push
```

Railway will automatically redeploy!

---

### **Step 8: Access Your Live App**

Your app is now live at:
```
https://road-tracker-production.up.railway.app/road-surfacing-tracker-realtime.html
```

**Test it:**
1. Open that URL in your browser
2. Create a new job
3. Click "Share Job" to get QR code
4. The QR code now works anywhere in the world!

---

## 🐛 Troubleshooting Railway Errors

### **Error: "Application failed to respond"**

**Check Railway Logs:**
1. In Railway dashboard, click your service
2. Click "Deployments" tab
3. Click the latest deployment
4. Check the logs for errors

**Common fixes:**
- Make sure `package.json` has `"start": "node server.js"`
- Verify `server.js` exists in your repository
- Check that all files were pushed to GitHub

---

### **Error: "Build failed"**

**Solution:**
1. Make sure you pushed ALL files (especially `package.json`)
2. Check GitHub repository - all files should be there
3. In Railway, click "Redeploy" to try again

---

### **Error: "404 Not Found" when accessing the URL**

**Check the correct URL format:**
```
✅ Correct: https://your-app.up.railway.app/road-surfacing-tracker-realtime.html
❌ Wrong:   https://your-app.up.railway.app/
```

You must include the HTML filename!

---

### **Error: "Unable to connect to server" in the app**

**Check API_URL in HTML file:**
```javascript
// Must match your Railway domain
const API_URL = 'https://YOUR-ACTUAL-DOMAIN.up.railway.app/api';
```

**Steps:**
1. Update the API_URL
2. Save the file
3. Run: `git add . && git commit -m "Fix API URL" && git push`
4. Wait for Railway to redeploy (~1 minute)

---

### **Error: "GET /api/jobs net::ERR_FAILED"**

This means CORS is blocking the request.

**Solution:** The server.js already has CORS enabled, but check:
1. Make sure you're using `https://` (not `http://`)
2. API_URL should NOT have trailing slash
3. Try clearing browser cache (Ctrl+Shift+Delete)

---

## 📝 Making Updates After Deployment

When you want to update your app:

```bash
# 1. Make your changes to the files
# 2. Add changes to git
git add .

# 3. Commit with a message
git commit -m "Describe what you changed"

# 4. Push to GitHub
git push

# Railway automatically redeploys!
```

---

## 💰 Railway Pricing

**Free Tier Includes:**
- $5 worth of usage per month
- 500 hours of runtime
- Good for testing and small projects

**When you exceed free tier:**
- You'll need to add a payment method
- Pay only for what you use (~$1-5/month for small apps)

**Monitor usage:**
- Railway dashboard → "Usage" tab

---

## 🔒 Making Your Repository Private (Optional)

After deployment, you can make your GitHub repo private:

1. Go to your GitHub repository
2. Click "Settings"
3. Scroll to "Danger Zone"
4. Click "Change visibility" → "Make private"

Railway will still have access!

---

## ✅ Quick Checklist

Before deploying, verify:

- [ ] All 7 files are in your folder
- [ ] Git is installed (`git --version` works)
- [ ] GitHub account created
- [ ] Repository created on GitHub
- [ ] Code pushed to GitHub (check github.com/yourusername/road-tracker)
- [ ] Railway connected to GitHub
- [ ] Deployment successful in Railway
- [ ] Domain generated in Railway
- [ ] API_URL updated in HTML file
- [ ] Updated HTML pushed to GitHub

---

## 🆘 Still Having Issues?

**Check these:**

1. **View Railway Logs:**
   - Railway Dashboard → Your Service → Deployments → Latest → Build Logs

2. **Verify GitHub:**
   - Go to github.com/yourusername/road-tracker
   - All files should be visible

3. **Test Server Locally First:**
   ```bash
   node server.js
   # Should say "Server running on http://localhost:3000"
   ```

4. **Common File Issues:**
   ```bash
   # Make sure these exact files exist:
   ls -la
   # Should show: server.js, package.json, railway.json, Procfile
   ```

---

## 📞 Getting Help

If you're still stuck, share:
1. Screenshot of Railway deployment page
2. Railway build logs (copy/paste the error)
3. Your GitHub repository URL
4. Screenshot of your file structure

I can help troubleshoot the specific issue!
