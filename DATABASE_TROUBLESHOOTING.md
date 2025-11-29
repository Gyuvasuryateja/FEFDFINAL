# Database Troubleshooting Guide

## Issue: "Error scheduling session" or Database Errors

If you're getting errors when trying to schedule sessions, it's likely because:

1. ✅ **Database tables don't exist** - You haven't run the schema.sql yet
2. ✅ **RLS (Row Level Security) policies blocking access**
3. ✅ **Date format issues** (Fixed in the code)

## Step 1: Verify Database Tables Exist

1. Go to your Supabase Dashboard: https://supabase.com
2. Select your project
3. Go to **SQL Editor** (left sidebar)
4. Run this query to check if the `sessions` table exists:

```sql
SELECT table_name 
FROM information_schema.tables 
WHERE table_schema = 'public' 
AND table_name = 'sessions';
```

**If it returns nothing**, the table doesn't exist. Continue to Step 2.

**If it returns a row**, the table exists. Check Step 3.

## Step 2: Create Database Tables

1. Go to **SQL Editor** in Supabase Dashboard
2. Copy the **ENTIRE** contents of `database/schema.sql` file
3. Paste it into the SQL Editor
4. Click **"Run"** or press `Ctrl+Enter`
5. Wait for success message

**Important**: This creates ALL tables including:
- ✅ `profiles` - User profiles
- ✅ `sessions` - Therapy sessions (THIS IS WHAT YOU NEED!)
- ✅ `resources` - Mental health resources
- ✅ `support_groups` - Support groups
- ✅ `forum_posts` - Forum posts
- ✅ All RLS policies

## Step 3: Verify RLS Policies

After creating tables, verify RLS policies exist:

1. Go to **SQL Editor**
2. Run this query:

```sql
SELECT tablename, policyname 
FROM pg_policies 
WHERE schemaname = 'public' 
AND tablename = 'sessions';
```

You should see policies like:
- "Users can view their own sessions"
- "Users can create their own sessions"
- "Admins can view all sessions"

## Step 4: Test Session Creation Manually

1. Go to **SQL Editor**
2. Get your user ID from **Authentication** → **Users** (copy the UUID)
3. Run this test query (replace `YOUR_USER_ID` with your actual UUID):

```sql
INSERT INTO public.sessions (
  student_id, 
  counselor_name, 
  session_date, 
  session_type, 
  status
) VALUES (
  'YOUR_USER_ID'::uuid,
  'Test Counselor',
  NOW() + INTERVAL '7 days',
  'individual',
  'scheduled'
);
```

**If this works**: The database is set up correctly, the issue is in the frontend.

**If this fails**: 
- Check error message
- Make sure you're using your actual user ID
- Verify RLS policies are created

## Step 5: Check Browser Console

1. Open your app in the browser
2. Press `F12` to open Developer Tools
3. Go to **Console** tab
4. Try to schedule a session
5. Look for error messages - they will tell you exactly what's wrong!

Common errors:
- `relation "public.sessions" does not exist` → Table doesn't exist (run schema.sql)
- `new row violates row-level security policy` → RLS policy issue
- `null value in column "student_id"` → Profile not loaded
- `invalid input syntax for type timestamp` → Date format issue (should be fixed now)

## Step 6: Verify Profile Exists

1. Go to **Table Editor** in Supabase Dashboard
2. Select `profiles` table
3. Check if your user profile exists

If not:
1. Go to **Authentication** → **Users**
2. Your profile should be auto-created by the trigger
3. If not, you may need to sign up again or manually create it

## Quick Fix Checklist

- [ ] Run `database/schema.sql` in Supabase SQL Editor
- [ ] Verify `sessions` table exists
- [ ] Verify RLS policies exist for `sessions` table
- [ ] Check browser console for specific errors
- [ ] Verify your user profile exists in `profiles` table
- [ ] Make sure you're logged in
- [ ] Try scheduling again

## Still Having Issues?

1. **Copy the exact error message** from browser console
2. **Check Supabase logs**: Dashboard → Logs → API Logs
3. **Verify environment variables** are set correctly in Vercel

The most common issue is: **Database tables don't exist** - Make sure you've run schema.sql!

