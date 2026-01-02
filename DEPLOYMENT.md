# 🚀 DEPLOYMENT GUIDE - Do Your Homework Media

## Quick Deploy Checklist

- [ ] Create GitHub account (if you don't have one)
- [ ] Create new repository
- [ ] Upload all files
- [ ] Enable GitHub Pages
- [ ] Configure Cloudflare DNS
- [ ] Add custom domain
- [ ] Enable HTTPS

---

## 📁 Files to Upload to GitHub

Upload these exact files:

1. **index.html** - Main website
2. **README.md** - Repository description
3. **CNAME** - Custom domain configuration
4. **404.html** - Error page
5. **robots.txt** - SEO configuration
6. **.gitignore** - Ignore unnecessary files

---

## STEP 1: Create GitHub Repository

1. Go to **github.com** and login
2. Click **"+"** (top right) → **"New repository"**
3. Repository name: `doyourhomework-media`
4. Make it **Public**
5. ✅ Check **"Add a README file"**
6. Click **"Create repository"**

---

## STEP 2: Upload Files

### Option A: Via GitHub Web Interface (Easiest)

1. Click **"uploading an existing file"** link
2. Drag and drop ALL 6 files listed above
3. Scroll down, click **"Commit changes"**

### Option B: Via Git Command Line

```bash
git clone https://github.com/YOUR-USERNAME/doyourhomework-media.git
cd doyourhomework-media
# Copy all files into this folder
git add .
git commit -m "Initial website deployment"
git push origin main
```

---

## STEP 3: Enable GitHub Pages

1. Go to repository **Settings**
2. Click **"Pages"** (left sidebar)
3. Under **"Source"**:
   - Branch: **main**
   - Folder: **/ (root)**
4. Click **"Save"**
5. Wait 1-2 minutes
6. Your site will be live at: `https://YOUR-USERNAME.github.io/doyourhomework-media/`

---

## STEP 4: Configure Cloudflare DNS

1. Login to **Cloudflare**
2. Select your domain: **doyourhomework.media**
3. Go to **DNS** section
4. Add these records:

### A Records (for root domain):
```
Type: A
Name: @
Content: 185.199.108.153
Proxy: ON (orange cloud)

Type: A
Name: @
Content: 185.199.109.153
Proxy: ON

Type: A
Name: @
Content: 185.199.110.153
Proxy: ON

Type: A
Name: @
Content: 185.199.111.153
Proxy: ON
```

### CNAME Record (for www):
```
Type: CNAME
Name: www
Content: YOUR-USERNAME.github.io
Proxy: ON (orange cloud)
```

---

## STEP 5: Add Custom Domain to GitHub

1. Back in GitHub → **Settings** → **Pages**
2. Under **"Custom domain"**:
   - Enter: `doyourhomework.media`
   - Click **"Save"**
3. Wait 5-10 minutes for DNS to propagate
4. ✅ Check **"Enforce HTTPS"**

---

## STEP 6: Verify Deployment

1. Visit: `https://doyourhomework.media`
2. Website should load with full cyberpunk design
3. Test the live chat
4. Check all sections load properly

---

## 🔄 Making Updates

Whenever you need to update the website:

1. Edit `index.html` locally
2. Go to GitHub repository
3. Click `index.html` → Click pencil icon (edit)
4. Paste new code
5. Click **"Commit changes"**
6. Wait 30-60 seconds → Changes are LIVE!

---

## ⚡ Troubleshooting

**Site not loading?**
- Wait 10 minutes for DNS propagation
- Clear browser cache (Ctrl+Shift+R)
- Check DNS records in Cloudflare

**Custom domain not working?**
- Verify CNAME file contains: `doyourhomework.media`
- Check GitHub Pages settings shows custom domain
- Ensure Cloudflare proxy is ON (orange cloud)

**HTTPS not working?**
- Wait 24 hours for certificate provisioning
- Ensure "Enforce HTTPS" is checked in GitHub Pages
- Set Cloudflare SSL to "Flexible" or "Full"

---

## 📞 Need Help?

Contact:
- spencer.romano@me.com
- justmetnadia@gmail.com

---

## 🎉 You're Live!

Once deployed, your website will be:
- ⚡ Lightning fast (Cloudflare CDN)
- 🔒 Secure (HTTPS enabled)
- 🌍 Global (Served worldwide)
- 💰 FREE (No hosting costs!)

**Welcome to the internet! 🚀**
