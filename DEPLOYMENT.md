# Deployment Guide - documentation.docuapi.io

This guide explains how to deploy the DocuAPI documentation to `documentation.docuapi.io` using Vercel and GoDaddy DNS.

## 📋 Prerequisites

- Vercel account (you already have one)
- Access to GoDaddy DNS management for docuapi.io
- This repository pushed to GitHub

## 🚀 Step 1: Deploy to Vercel

### Option A: Via Vercel Dashboard (Recommended)

1. **Go to Vercel Dashboard**
   - Visit [https://vercel.com/dashboard](https://vercel.com/dashboard)
   - Click "Add New..." → "Project"

2. **Import Git Repository**
   - Select "Import Git Repository"
   - Choose `orhanbiler/pdf-api-docu` from your GitHub repos
   - Click "Import"

3. **Configure Project**
   - **Framework Preset**: Other (or leave as Auto-detect)
   - **Build Command**: `pnpm build`
   - **Output Directory**: `build`
   - **Install Command**: `pnpm install`
   - Click "Deploy"

4. **Add Custom Domain**
   - After deployment, go to "Settings" → "Domains"
   - Add domain: `documentation.docuapi.io`
   - Vercel will provide DNS records to add

### Option B: Via Vercel CLI

```bash
# Install Vercel CLI if not already installed
npm i -g vercel

# In your project directory
cd pdf-api-docu

# Deploy to Vercel
vercel

# Follow prompts:
# - Set up and deploy: Y
# - Which scope: (select your account)
# - Link to existing project: N
# - Project name: pdf-api-docu
# - Directory: ./
# - Build Command: pnpm build
# - Output Directory: build
# - Development Command: pnpm start

# Add custom domain
vercel domains add documentation.docuapi.io
```

## 🌐 Step 2: Configure DNS in GoDaddy

### Add CNAME Record

1. **Login to GoDaddy**
   - Go to [https://godaddy.com](https://godaddy.com)
   - Navigate to "My Products" → "DNS" for docuapi.io

2. **Add CNAME Record**
   ```
   Type: CNAME
   Name: documentation
   Value: cname.vercel-dns.com
   TTL: 600 seconds (or use default)
   ```

3. **Save Changes**
   - Click "Save" to apply DNS changes
   - DNS propagation can take 5-48 hours (usually much faster)

### Alternative: A Record (if CNAME doesn't work)

If you need to use an A record instead:
```
Type: A
Name: documentation
Value: 76.76.21.21
TTL: 600 seconds
```

## ✅ Step 3: Verify Deployment

1. **Check DNS Propagation**
   - Visit [https://dnschecker.org](https://dnschecker.org)
   - Enter `documentation.docuapi.io`
   - Verify it points to Vercel

2. **Verify in Vercel**
   - Go to your project in Vercel Dashboard
   - Check "Domains" section
   - Should show ✓ next to `documentation.docuapi.io`

3. **Test the Site**
   - Visit [https://documentation.docuapi.io](https://documentation.docuapi.io)
   - Should load your documentation site with SSL

## 🔄 Continuous Deployment

With Vercel connected to GitHub:
- **Automatic Deployments**: Every push to `main` branch triggers a new deployment
- **Preview Deployments**: Pull requests get preview URLs automatically
- **Rollback**: Can instantly rollback to previous deployments in Vercel dashboard

## 🛠️ Environment Variables (if needed)

In Vercel Dashboard → Settings → Environment Variables:
```
# Add any environment variables here if needed
# Example:
NEXT_PUBLIC_API_URL=https://docuapi.io/api
```

## 📝 Important Notes

1. **SSL Certificate**: Vercel automatically provisions SSL certificates via Let's Encrypt
2. **WWW Subdomain**: If you want `www.documentation.docuapi.io`, add another CNAME record
3. **Apex Domain**: The main `docuapi.io` should remain pointing to your current hosting
4. **Build Cache**: Vercel caches dependencies for faster builds

## 🚨 Troubleshooting

### Domain Not Working
- Wait for DNS propagation (up to 48 hours, usually faster)
- Clear browser cache and try incognito mode
- Check DNS records in GoDaddy are correct
- Verify domain in Vercel dashboard shows as configured

### Build Failures
- Check build logs in Vercel dashboard
- Ensure `pnpm-lock.yaml` is committed
- Verify Node.js version compatibility (18.0+)

### 404 Errors
- The `vercel.json` includes rewrites for SPA routing
- If issues persist, check Docusaurus baseUrl config

## 📞 Support

- **Vercel Support**: [https://vercel.com/support](https://vercel.com/support)
- **GoDaddy Support**: [https://www.godaddy.com/help](https://www.godaddy.com/help)
- **Docusaurus Docs**: [https://docusaurus.io/docs](https://docusaurus.io/docs)

---

After completing these steps, your documentation will be live at:
**https://documentation.docuapi.io**
