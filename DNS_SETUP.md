# DNS Configuration Fix for documentation.docuapi.io

## Current Status
✅ Vercel deployment is working (pdf-api-docu.vercel.app)  
❌ Custom domain showing "Invalid Configuration"  
➡️ Need to configure DNS in GoDaddy

## Step 1: Click "View DNS Records & More for docuapi.io"

Click the blue link in Vercel that says "View DNS Records & More for docuapi.io →"

This will show you EXACTLY what DNS records Vercel needs you to add.

## Step 2: What Vercel Will Show You

Vercel will likely show one of these options:

### Option A: CNAME Record (Most Common)
```
Type: CNAME
Name: documentation
Value: cname.vercel-dns.com
TTL: 3600 (or leave default)
```

### Option B: A Record (Alternative)
```
Type: A
Name: documentation
Value: 76.76.21.21
TTL: 3600
```

## Step 3: Add Records in GoDaddy

1. **Login to GoDaddy**
   - Go to https://dcc.godaddy.com/control/docuapi.io/dns
   - Or navigate: My Products → Domain → docuapi.io → DNS

2. **Add the DNS Record**
   
   For CNAME (recommended):
   - Click "Add" or "Add Record"
   - Type: `CNAME`
   - Name: `documentation` (just this, not the full domain)
   - Value: `cname.vercel-dns.com`
   - TTL: Leave default or set to 600
   - Click "Save"

   For A Record (if CNAME doesn't work):
   - Click "Add" or "Add Record"
   - Type: `A`
   - Name: `documentation`
   - Value: `76.76.21.21`
   - TTL: Leave default or set to 600
   - Click "Save"

## Step 4: Wait and Verify

1. **DNS Propagation**: Usually takes 5-30 minutes, can take up to 48 hours
2. **Check Status**: 
   - Refresh the Vercel domains page
   - Click "Refresh" button next to documentation.docuapi.io
   - It should change from "Invalid Configuration" to "Valid Configuration" ✅

## Step 5: Troubleshooting

If still showing "Invalid Configuration" after 30 minutes:

### Check Existing Records
In GoDaddy, make sure there's no conflicting record:
- No existing A record for "documentation"
- No existing CNAME for "documentation"
- Delete any conflicting records before adding the new one

### Try Alternative Method
If CNAME doesn't work, try A record (or vice versa)

### Verify in Terminal
```bash
# Check DNS resolution
nslookup documentation.docuapi.io

# Or use dig
dig documentation.docuapi.io
```

### Clear DNS Cache
On your Mac:
```bash
sudo dscacheutil -flushcache
```

## Common Issues & Solutions

### Issue: "Name already exists"
**Solution**: You have an existing record for "documentation". Delete it first, then add the new one.

### Issue: Still shows invalid after hours
**Solution**: 
1. Double-check the record in GoDaddy matches EXACTLY what Vercel shows
2. Make sure you didn't add the full domain in the "Name" field (just "documentation", not "documentation.docuapi.io")
3. Try removing and re-adding the domain in Vercel

### Issue: SSL Certificate Error
**Solution**: This auto-resolves once DNS is properly configured. Vercel will provision SSL automatically.

## Expected Final Result

Once properly configured:
- ✅ documentation.docuapi.io shows "Valid Configuration" 
- ✅ SSL certificate automatically provisioned
- ✅ Site accessible at https://documentation.docuapi.io
- ✅ Automatic deployments on git push

## Quick Checklist

- [ ] Clicked "View DNS Records" in Vercel to see exact requirements
- [ ] Logged into GoDaddy DNS management
- [ ] Added CNAME or A record as shown by Vercel
- [ ] Name field contains only "documentation" (not full domain)
- [ ] Waited 5-30 minutes for propagation
- [ ] Refreshed Vercel domains page to check status

---

**Need the exact DNS values?** Click the "View DNS Records & More for docuapi.io →" link in your Vercel dashboard screenshot - it will show you the exact values to add!
