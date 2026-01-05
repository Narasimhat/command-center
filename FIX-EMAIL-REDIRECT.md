# 🔧 Fix Email Confirmation Redirect (localhost → GitHub Pages)

## Problem
Supabase confirmation emails are redirecting to `localhost` instead of your GitHub Pages URL.

## ✅ Solution: Update Supabase Settings

### Step 1: Go to Supabase Dashboard
1. Go to https://supabase.com/dashboard
2. Select your project
3. Click **Authentication** (left sidebar)
4. Click **URL Configuration**

### Step 2: Add Your GitHub Pages URL

Under **"Redirect URLs"**, add:
```
https://Narasimhat.github.io/command-center/
```

Also add (for development):
```
http://localhost:*
```

Click **"Save"**

### Step 3: Update Site URL (Optional but Recommended)

Under **"Site URL"**, set it to:
```
https://Narasimhat.github.io/command-center/
```

Click **"Save"**

## ✅ Solution: Code Already Updated

I've already updated the code to automatically use the current URL for email redirects. The code now uses:
```javascript
const redirectUrl = window.location.origin + window.location.pathname;
```

This means:
- On GitHub Pages: `https://Narasimhat.github.io/command-center/`
- On localhost: `http://localhost:...` (for development)

## 🧪 Test It

1. **Sign out** if you're signed in
2. **Sign up** with a new email
3. **Check your email** - the confirmation link should now go to your GitHub Pages URL
4. **Click the link** - it should redirect to your app and sign you in

## 📝 What Changed

- ✅ Code now automatically detects the current URL
- ✅ Email redirects will use the correct URL
- ✅ Works on both GitHub Pages and localhost

## 🆘 Still Not Working?

1. **Clear browser cache** and try again
2. **Check Supabase logs**: Dashboard → Logs → Auth
3. **Verify URL** in Supabase settings matches exactly (no trailing slash issues)
4. **Try signing up again** after updating settings

---

**After updating Supabase settings, new signups will use the correct redirect URL!** ✅

