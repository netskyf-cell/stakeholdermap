# StakeholderMap — Vercel Deployment Guide

Everything you need, step by step, with every click spelled out.

Total time: ~20 minutes. Zero coding required.

---

## What you're setting up

Think of it as three puzzle pieces clicking together:

- **GitHub** = your file storage (like a Google Drive for code)
- **Vercel** = the host that makes your app available on the internet (like Wix, but for apps)
- **Anthropic API key** = the power source for the AI features

Once connected, any change you make in GitHub automatically updates your live app. Magic.

---

## STEP 1: Get your Anthropic API key (3 min)

You need this for the AI features (strategy briefs, bulk import, message drafting).

1. Go to **https://console.anthropic.com**
2. Click **Sign up** (or log in if you have an account)
3. Once inside, click **API Keys** in the left sidebar (or go to https://console.anthropic.com/settings/keys)
4. Click **Create Key**
5. Give it a name like `stakeholdermap`
6. **COPY the key immediately** — it starts with `sk-ant-...`
7. Paste it somewhere safe (a notes app, a password manager). You'll need it in Step 4.

**Cost:** You need to add credits. $5 (about €4.50) will last you months. Go to **Plans & Billing** to add credits.

---

## STEP 2: Create a GitHub account and repository (5 min)

### 2a. Create a GitHub account (skip if you have one)

1. Go to **https://github.com**
2. Click **Sign up**
3. Enter your email, create a password, choose a username
4. Verify your email

### 2b. Create a new repository

1. Once logged in, click the **+** icon (top-right corner) → **New repository**
2. Fill in:
   - **Repository name:** `stakeholdermap`
   - **Description:** `AI-powered stakeholder analysis tool`
   - **Visibility:** select **Public** (Vercel's free tier needs this)
   - Check **Add a README file**
3. Click **Create repository**

### 2c. Upload your project files

1. You should now see your new repository page
2. Click **Add file** → **Upload files**
3. From the `stakeholdermap-vercel` folder I gave you, drag ALL these files and folders into the upload area:
   - `api/` (the whole folder — contains `ai.js`)
   - `public/` (the whole folder — contains `index.html`)
   - `package.json`
   - `vercel.json`
   - `.gitignore`
4. At the bottom, click **Commit changes**

**Important:** Make sure the structure looks like this in GitHub:

```
stakeholdermap/
├── api/
│   └── ai.js
├── public/
│   └── index.html
├── package.json
├── vercel.json
├── .gitignore
└── README.md
```

If `api/ai.js` ended up as just `ai.js` in the root, you need to recreate it inside the `api` folder. To do this:
1. Click **Add file** → **Create new file**
2. In the filename field, type: `api/ai.js` (typing the slash creates the folder automatically)
3. Paste the contents of `ai.js` into the editor
4. Click **Commit changes**

---

## STEP 3: Connect Vercel to GitHub (5 min)

1. Go to **https://vercel.com**
2. Click **Sign Up** → choose **Continue with GitHub**
3. Authorize Vercel to access your GitHub account
4. You'll land on the Vercel dashboard

### Deploy your project

1. Click **Add New...** → **Project**
2. You'll see a list of your GitHub repos. Find **stakeholdermap** and click **Import**
3. On the configuration page:
   - **Framework Preset:** leave as `Other`
   - **Root Directory:** leave blank (it's the repo root)
   - **Build Command:** leave empty
   - **Output Directory:** leave as `public`
4. **DO NOT click Deploy yet** — you need to add your API key first (Step 4)

---

## STEP 4: Add your API key to Vercel (2 min)

Still on the Vercel project configuration page (before deploying):

1. Expand the **Environment Variables** section
2. Add a new variable:
   - **Key:** `ANTHROPIC_API_KEY`
   - **Value:** paste your API key from Step 1 (the one starting with `sk-ant-...`)
3. Make sure all three environment checkboxes are ticked: **Production**, **Preview**, **Development**
4. Click **Add**

Now click **Deploy**

---

## STEP 5: Wait and celebrate (2 min)

1. Vercel will build and deploy your app. This takes about 30–60 seconds.
2. When it says **Congratulations!** you're done.
3. Click the preview image or the URL to see your live app.

Your app is now live at something like: **https://stakeholdermap.vercel.app**

---

## STEP 6: Custom domain (optional, 5 min)

To use your own domain like `stakeholdermap.app`:

### 6a. Buy a domain

1. Go to **https://namecheap.com** (or any domain registrar)
2. Search for your domain (e.g., `stakeholdermap.app`, `stakeholdermap.io`)
3. Buy it (~€12/year)

### 6b. Connect it to Vercel

1. In your Vercel dashboard, go to your project → **Settings** → **Domains**
2. Type your domain name and click **Add**
3. Vercel will show you DNS records to add. Go to your domain registrar (Namecheap):
   - Log in → **Domain List** → click **Manage** next to your domain
   - Go to **Advanced DNS**
   - Add the records Vercel tells you to (usually an A record and/or CNAME)
4. Wait 5–30 minutes for DNS to propagate
5. Vercel will show a green checkmark when it's ready

---

## How to update the app later

Whenever you want to change something:

1. Go to your GitHub repo (https://github.com/YOUR_USERNAME/stakeholdermap)
2. Navigate to the file you want to change
3. Click the **pencil icon** (edit)
4. Make your changes
5. Click **Commit changes**

Vercel automatically detects the change and redeploys in ~30 seconds. You don't have to do anything else.

Or: come back to Claude and ask me to generate an updated file. Then upload it to GitHub.

---

## Troubleshooting

### "AI features don't work"
- Go to Vercel → your project → **Settings** → **Environment Variables**
- Check that `ANTHROPIC_API_KEY` is there and starts with `sk-ant-...`
- If you just added or changed it, click **Redeploy** in the **Deployments** tab

### "Page shows blank white screen"
- Check that `public/index.html` exists in your GitHub repo
- Check Vercel → your project → **Deployments** → click the latest → **Functions** tab for errors

### "I get a 404 error"
- Make sure `vercel.json` is in the root of your repo (not inside a folder)
- Check that the **Output Directory** in Vercel project settings is set to `public`

### "Bulk import doesn't parse correctly"
- Make sure your Anthropic account has credits (https://console.anthropic.com → Billing)
- The function may time out for very large lists — try 10 stakeholders at a time

### "I want to change a feature"
- Come back to this Claude conversation and ask. I can generate updated files that you just upload to GitHub.

---

## Cost summary

| Item | Cost | Frequency |
|------|------|-----------|
| Vercel hosting | Free | Forever (hobby plan) |
| GitHub | Free | Forever |
| Domain name | ~€12 | Per year (optional) |
| Anthropic API | ~€5 | Per month (for ~1,500 AI queries) |
| **Total** | **€5–6/month** | |

Your revenue target is €1,000/month. Your costs are under €6/month. That's a 99.4% margin.
