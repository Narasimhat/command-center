# 🚀 Supabase Integration Setup Guide

Complete guide to set up automatic cloud sync using Supabase.

## 📋 Prerequisites

- A Supabase account (free at https://supabase.com)
- Your Supabase project URL and API key

## 🔧 Step 1: Create Supabase Table

1. **Go to your Supabase Dashboard**
   - Navigate to **Table Editor**
   - Click **"New Table"**

2. **Create the `calendar_data` table:**
   - **Table name:** `calendar_data`
   - **Description:** "Stores user calendar data"

3. **Add Columns:**
   
   | Column Name | Type | Default | Nullable | Primary Key |
   |------------|------|---------|----------|-------------|
   | `user_id` | `uuid` | - | No | ✅ Yes |
   | `data` | `jsonb` | - | No | No |
   | `updated_at` | `timestamptz` | `now()` | No | No |

4. **Set up Row Level Security (RLS):**
   - Go to **Authentication** → **Policies**
   - Click **"New Policy"** for `calendar_data` table
   - **Policy name:** "Users can only access their own data"
   - **Policy definition:**
     ```sql
     -- Enable RLS
     ALTER TABLE calendar_data ENABLE ROW LEVEL SECURITY;
     
     -- Create policy for SELECT
     CREATE POLICY "Users can view own data"
     ON calendar_data FOR SELECT
     USING (auth.uid() = user_id);
     
     -- Create policy for INSERT
     CREATE POLICY "Users can insert own data"
     ON calendar_data FOR INSERT
     WITH CHECK (auth.uid() = user_id);
     
     -- Create policy for UPDATE
     CREATE POLICY "Users can update own data"
     ON calendar_data FOR UPDATE
     USING (auth.uid() = user_id)
     WITH CHECK (auth.uid() = user_id);
     
     -- Create policy for DELETE (optional)
     CREATE POLICY "Users can delete own data"
     ON calendar_data FOR DELETE
     USING (auth.uid() = user_id);
     ```

## 🔑 Step 2: Get Your Supabase Credentials

1. **Go to Project Settings**
   - Click the gear icon (⚙️) in left sidebar
   - Select **"API"**

2. **Copy Your Credentials:**
   - **Project URL:** `https://xxxxx.supabase.co`
   - **anon/public key:** The `anon` key (starts with `eyJ...`)

## ⚙️ Step 3: Configure the App

1. **Open `index.html`**

2. **Find the Supabase Configuration** (around line 2708):
   ```javascript
   const supabaseConfig = {
       url: 'YOUR_SUPABASE_URL', // e.g., https://xxxxx.supabase.co
       anonKey: 'YOUR_SUPABASE_ANON_KEY'
   };
   ```

3. **Replace with your credentials:**
   ```javascript
   const supabaseConfig = {
       url: 'https://your-project-id.supabase.co',
       anonKey: 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...'
   };
   ```

4. **Save the file**

## 🎯 Step 4: Enable Real-time Sync (Optional)

1. **Go to Database → Replication**
2. **Enable replication for `calendar_data` table**
3. This allows real-time updates across devices

## ✅ Step 5: Test the Integration

1. **Open your app** in a browser
2. **Click the 👤 button** (top right) to sign in
3. **Enter your email** and password
4. **If account doesn't exist**, it will create one
5. **Check the sync status** - should show "Synced" ☁️

## 🔄 How It Works

- **Sign In:** Click 👤 button, enter email/password
- **Auto Sync:** All changes automatically sync to Supabase
- **Real-time:** Changes on one device appear on others instantly
- **Offline:** Works offline, syncs when connection restored

## 🛠️ Troubleshooting

### "Table not found" error
- Make sure table name is exactly `calendar_data`
- Check you're in the correct Supabase project

### "Permission denied" error
- Enable Row Level Security (RLS) policies
- Make sure policies allow users to access their own data

### "Invalid API key" error
- Double-check your `anonKey` is correct
- Make sure you copied the full key (it's long!)

### Sync not working
- Check browser console (F12) for errors
- Verify you're signed in (👤 button should show 👋)
- Check Supabase dashboard → Logs for errors

## 📊 Database Schema

```sql
CREATE TABLE calendar_data (
    user_id UUID PRIMARY KEY REFERENCES auth.users(id),
    data JSONB NOT NULL,
    updated_at TIMESTAMPTZ DEFAULT NOW()
);

-- Create index for faster queries
CREATE INDEX idx_calendar_data_user_id ON calendar_data(user_id);

-- Auto-update updated_at timestamp
CREATE OR REPLACE FUNCTION update_updated_at_column()
RETURNS TRIGGER AS $$
BEGIN
    NEW.updated_at = NOW();
    RETURN NEW;
END;
$$ language 'plpgsql';

CREATE TRIGGER update_calendar_data_updated_at
    BEFORE UPDATE ON calendar_data
    FOR EACH ROW
    EXECUTE FUNCTION update_updated_at_column();
```

## 🔒 Security Notes

- **RLS is enabled** - Users can only see their own data
- **Anon key is safe** - It's public, but RLS protects your data
- **No server code needed** - Everything runs in the browser
- **HTTPS required** - Supabase requires secure connections

## 🎉 You're Done!

Your app now has automatic cloud sync! 

- ✅ Sign in on any device
- ✅ Data syncs automatically
- ✅ Real-time updates
- ✅ Works offline
- ✅ Secure and private

---

**Need Help?** Check the Supabase docs: https://supabase.com/docs

