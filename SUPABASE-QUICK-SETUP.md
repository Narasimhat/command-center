# ⚡ Quick Supabase Setup (2 Minutes)

## ✅ Step 1: Get Your Anon Key

1. Go to your Supabase Dashboard: https://supabase.com/dashboard
2. Select your project (or create one if you don't have one)
3. Click **Settings** (⚙️ icon) in the left sidebar
4. Click **API** in the settings menu
5. Find **"Project API keys"** section
6. Copy the **`anon` `public`** key (it's a long string starting with `eyJ...`)

## ✅ Step 2: Update index.html

1. Open `index.html` in a text editor
2. Find this section (around line 2708):

```javascript
const supabaseConfig = {
    url: 'https://ghfnrwwsdsabpmicwnnv.supabase.co', // ✅ Already set!
    anonKey: 'YOUR_SUPABASE_ANON_KEY' // ⬅️ Replace this!
};
```

3. Replace `YOUR_SUPABASE_ANON_KEY` with your actual anon key:

```javascript
const supabaseConfig = {
    url: 'https://ghfnrwwsdsabpmicwnnv.supabase.co',
    anonKey: 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6ImdoZm5yd3dzZHNhYnBtaWN3bm52Iiwicm9sZSI6ImFub24iLCJpYXQiOjE3M...' // Your actual key
};
```

## ✅ Step 3: Create Database Table

1. In Supabase Dashboard, go to **SQL Editor** (left sidebar)
2. Click **"New query"**
3. Paste this SQL and click **"Run"**:

```sql
-- Create the table
CREATE TABLE IF NOT EXISTS calendar_data (
    user_id UUID PRIMARY KEY REFERENCES auth.users(id),
    data JSONB NOT NULL,
    updated_at TIMESTAMPTZ DEFAULT NOW()
);

-- Enable Row Level Security
ALTER TABLE calendar_data ENABLE ROW LEVEL SECURITY;

-- Create policies (users can only access their own data)
CREATE POLICY "Users can view own data"
ON calendar_data FOR SELECT
USING (auth.uid() = user_id);

CREATE POLICY "Users can insert own data"
ON calendar_data FOR INSERT
WITH CHECK (auth.uid() = user_id);

CREATE POLICY "Users can update own data"
ON calendar_data FOR UPDATE
USING (auth.uid() = user_id)
WITH CHECK (auth.uid() = user_id);

CREATE POLICY "Users can delete own data"
ON calendar_data FOR DELETE
USING (auth.uid() = user_id);
```

4. You should see "Success. No rows returned"

## ✅ Step 4: Test It!

1. Open your `index.html` in a browser
2. Click the **👤 button** (top right)
3. Enter your email and password
4. If account doesn't exist, it will create one
5. Check sync status - should show **"Synced" ☁️**

## 🎉 Done!

Your app now syncs automatically across all devices!

---

**Where to find things in Supabase:**

- **URL:** Already in your code ✅
- **Anon Key:** Settings → API → `anon` `public` key
- **SQL Editor:** Left sidebar → SQL Editor
- **Table Editor:** Left sidebar → Table Editor (to verify table was created)

**Troubleshooting:**
- If you see "Table not found" → Make sure you ran the SQL to create the table
- If you see "Permission denied" → Make sure you created the RLS policies
- If sync doesn't work → Check browser console (F12) for errors

