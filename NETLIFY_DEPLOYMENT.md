# Netlify Deployment Guide

## Issue Fixed: Blank Page Problem

The blank page was caused by missing Netlify configuration. This has been fixed by adding `netlify.toml`.

## Step 1: Configure Environment Variables in Netlify

Your application requires Supabase environment variables. You **must** add these in Netlify:

1. Go to your Netlify dashboard: https://app.netlify.com
2. Select your site (deft-dolphin-39446f)
3. Go to **Site settings** → **Environment variables**
4. Add the following variables:

   ```
   VITE_SUPABASE_URL=your_supabase_url_here
   VITE_SUPABASE_ANON_KEY=your_supabase_anon_key_here
   ```

### How to Find Your Supabase Values:

1. Go to https://supabase.com and sign in
2. Select your project
3. Go to **Settings** → **API**
4. Copy:
   - **Project URL** → This is your `VITE_SUPABASE_URL`
   - **anon/public key** → This is your `VITE_SUPABASE_ANON_KEY`

### Adding Variables in Netlify:

1. Click **"Add a variable"** in the Environment variables section
2. For each variable:
   - **Key**: `VITE_SUPABASE_URL` (or `VITE_SUPABASE_ANON_KEY`)
   - **Value**: Paste your actual value
   - **Scopes**: Select **"All scopes"** (or just **"Production"**)
3. Click **"Save"**

## Step 2: Trigger a New Deployment

After adding environment variables:

1. Go to **Deploys** tab in Netlify
2. Click **"Trigger deploy"** → **"Deploy site"**
3. This will rebuild your site with the new environment variables

OR

If you have auto-deploy enabled from GitHub:
- Just push any commit to your repository
- Netlify will automatically redeploy

## Step 3: Verify the Fix

1. After deployment completes, visit your site
2. Open browser console (F12)
3. You should see: `✅ Supabase connection successful!`
4. The page should no longer be blank

## Netlify Configuration

The `netlify.toml` file has been added with:
- Build command: `npm run build`
- Publish directory: `dist`
- SPA redirect rules (for React Router)

## Troubleshooting

### Still seeing blank page?

1. **Check browser console** (F12) for errors
2. **Verify environment variables** are set correctly in Netlify
3. **Check deployment logs** in Netlify dashboard → Deploys → Click on latest deploy
4. **Make sure variables start with `VITE_`** (this is required for Vite)

### Common Errors:

- **"Missing Supabase environment variables"** → Environment variables not set in Netlify
- **Build failed** → Check build logs for specific errors
- **404 on routes** → SPA redirect should fix this (already configured in netlify.toml)

## Next Steps

1. ✅ Add environment variables in Netlify
2. ✅ Trigger new deployment
3. ✅ Test your application

Your application should now work correctly on Netlify!

