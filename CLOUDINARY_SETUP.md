# Cloudinary Setup for File Uploads

Since Firebase Storage isn't available in your region's free tier, we're using **Cloudinary** instead - completely free with 25GB storage!

## Quick Setup (5 minutes)

### Step 1: Create Free Cloudinary Account

1. Go to: https://cloudinary.com/users/register_free
2. Sign up with your email: **gitesh.aggarwal489@gmail.com**
3. Verify your email
4. Login to your dashboard

### Step 2: Get Your Cloud Name

1. In Cloudinary dashboard, look at the top
2. You'll see: **Cloud Name: xxxxxxxx**
3. Copy this cloud name (e.g., `dxxxxxxxx`)

### Step 3: Create Upload Preset

1. In Cloudinary dashboard, go to: **Settings** (gear icon)
2. Click **Upload** tab
3. Scroll down to **Upload presets**
4. Click **Add upload preset**
5. Configure:
   - **Preset name:** `gitesh_checklist_uploads`
   - **Signing mode:** Select **Unsigned**
   - **Folder:** `gitesh-checklist`
   - Leave everything else as default
6. Click **Save**
7. Copy the preset name: `gitesh_checklist_uploads`

### Step 4: Update Your App Config

1. Open `index.html` in your editor
2. Find this section (around line 675):

```javascript
const CLOUDINARY_CONFIG = {
    cloudName: 'YOUR_CLOUD_NAME',
    uploadPreset: 'YOUR_UPLOAD_PRESET'
};
```

3. Replace with your actual values:

```javascript
const CLOUDINARY_CONFIG = {
    cloudName: 'dxxxxxxxx',  // Your cloud name from Step 2
    uploadPreset: 'gitesh_checklist_uploads'  // Preset name from Step 3
};
```

### Step 5: Deploy

```bash
cd C:\Users\gites\gitesh-simple-checklist
git add index.html
git commit -m "Configure Cloudinary for file uploads"
git push origin master
firebase deploy --only hosting
```

## Done!

Your app now supports:
- ✅ Images (all sizes)
- ✅ PDFs
- ✅ Videos
- ✅ Documents (all types)
- ✅ 25GB free storage
- ✅ Fast CDN delivery worldwide

Test at: https://gitesh-simple.web.app

## Cloudinary Features (All Free)

- **Storage:** 25GB
- **Bandwidth:** 25GB/month
- **Transformations:** 25k/month
- **Image optimization:** Automatic
- **CDN:** Global delivery
- **No credit card required**

## Troubleshooting

### "Cloudinary not configured" error
- Make sure you replaced `YOUR_CLOUD_NAME` and `YOUR_UPLOAD_PRESET` in `index.html`

### Upload fails with "Invalid signature"
- Check that your upload preset signing mode is set to **Unsigned**

### "Preset not found"
- Verify the preset name matches exactly (case-sensitive)

## Alternative: Quick Test Config

If you want to test immediately, I can set up a temporary Cloudinary account for testing. Let me know!
