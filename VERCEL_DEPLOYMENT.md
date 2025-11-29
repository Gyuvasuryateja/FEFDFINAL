# Vercel Deployment Guide

## Quick Deploy to Vercel (Free Tier)

Vercel offers a generous free tier that's perfect for this project. Follow these steps:

## Method 1: Deploy via Vercel Dashboard (Recommended)

### Step 1: Prepare Your Repository

✅ Your code is already on GitHub at: `https://github.com/Gyuvasuryateja/FEFDFINAL.git`

### Step 2: Deploy to Vercel

1. Go to **https://vercel.com** and sign up/login (use GitHub to sign in - it's free)
2. Click **"Add New Project"** or **"Import Project"**
3. Import your GitHub repository:
   - Select **"Import Git Repository"**
   - Find and select: **`Gyuvasuryateja/FEFDFINAL`**
   - Or paste: `https://github.com/Gyuvasuryateja/FEFDFINAL.git`
   - Click **"Import"**

### Step 3: Configure Project Settings

Vercel should auto-detect your Vite project. **IMPORTANT**: Set these settings:

- **Framework Preset**: Vite (should be auto-detected)
- **Root Directory**: Click "Edit" → Type `hackathaon` (since your project is in this subdirectory)
- **Build Command**: `npm run build` (should auto-fill)
- **Output Directory**: `dist` (should auto-fill)
- **Install Command**: `npm install` (should auto-fill)

**Note**: Since your project files are in the `hackathaon` folder, you MUST set the Root Directory to `hackathaon` in Vercel settings!

### Step 4: Add Environment Variables

**IMPORTANT**: You must add your Supabase environment variables!

1. In the project configuration, scroll to **"Environment Variables"**
2. Click **"Add"** and add these two variables:

   ```
   VITE_SUPABASE_URL = (your Supabase project URL)
   VITE_SUPABASE_ANON_KEY = (your Supabase anon key)
   ```

   **How to find your Supabase values:**
   - Go to https://supabase.com → Your project
   - Go to **Settings** → **API**
   - Copy:
     - **Project URL** → `VITE_SUPABASE_URL`
     - **anon/public key** → `VITE_SUPABASE_ANON_KEY`

3. Make sure to add them for **Production**, **Preview**, and **Development** environments

### Step 5: Deploy

1. Click **"Deploy"** button
2. Wait for the build to complete (usually 1-2 minutes)
3. Once done, you'll get a URL like: `https://your-project.vercel.app`

### Step 6: Verify

1. Visit your deployment URL
2. Open browser console (F12)
3. You should see: `✅ Supabase connection successful!`
4. The app should load correctly!

---

## Method 2: Deploy via Vercel CLI (Alternative)

If you prefer command line:

```bash
# Install Vercel CLI globally
npm install -g vercel

# Navigate to your project
cd hackathaon

# Deploy
vercel

# Follow the prompts:
# - Set up and deploy? Y
# - Link to existing project? N
# - Project name? (press enter for default)
# - Directory? (press enter, or type 'hackathaon' if needed)
# - Override settings? N

# Add environment variables
vercel env add VITE_SUPABASE_URL
vercel env add VITE_SUPABASE_ANON_KEY

# Redeploy with environment variables
vercel --prod
```

---

## Configuration Files

The `vercel.json` file has been configured with:
- ✅ Build command: `npm run build`
- ✅ Output directory: `dist`
- ✅ SPA routing rewrites (for React Router)

---

## Vercel Free Tier Benefits

- ✅ Unlimited personal projects
- ✅ 100GB bandwidth per month
- ✅ Automatic HTTPS
- ✅ Custom domains
- ✅ Automatic deployments on git push
- ✅ Preview deployments for pull requests
- ✅ No credit card required

---

## Troubleshooting

### Still seeing blank page?

1. **Check build logs** in Vercel dashboard → Deployments → Click on deployment
2. **Verify environment variables** are set correctly
3. **Check browser console** (F12) for errors
4. **Make sure variables start with `VITE_`** prefix

### Build Fails?

- Check that `node_modules` is NOT committed to git (it's in .gitignore - good!)
- Verify `package.json` has correct build script: `"build": "vite build"`

### Routes Not Working?

- The `vercel.json` rewrites should handle this
- If not, verify the rewrites section is correct

### Environment Variables Not Working?

1. Make sure you added them in Vercel dashboard
2. Redeploy after adding variables (Vercel should auto-redeploy)
3. Variables must start with `VITE_` to be accessible in Vite apps

---

## Next Steps After Deployment

1. ✅ Your app is live on Vercel!
2. 🔗 Share your deployment URL
3. 🔄 Every push to GitHub will auto-deploy
4. 📊 Monitor deployments in Vercel dashboard

---

## Comparing Netlify vs Vercel (Free Tier)

| Feature | Netlify Free | Vercel Free |
|---------|-------------|-------------|
| Builds per month | 300 | Unlimited |
| Bandwidth | 100GB | 100GB |
| Team members | 1 | Unlimited |
| Custom domains | ✅ | ✅ |
| Auto HTTPS | ✅ | ✅ |
| Preview deployments | ✅ | ✅ |

**Verdict**: Vercel free tier is excellent for this project! 🚀

---

Need help? Check Vercel docs: https://vercel.com/docs

