# 🚀 Quick Deployment Checklist

## Pre-Deployment Steps

### 1. Environment Setup
- [ ] Copy `.env.example` to `.env`
- [ ] Add your Gemini API key to `.env`
- [ ] Add your Formspree endpoint to `.env`
- [ ] Test locally with `pnpm dev`

### 2. Build Test
```bash
# Test build locally
pnpm build
pnpm preview
```

### 3. Git Preparation
```bash
# Commit all changes
git add .
git commit -m "Deploy to Netlify"
git push origin main
```

## Netlify Deployment

### Quick Deploy (5 minutes)

1. **Go to Netlify**: [app.netlify.com](https://app.netlify.com)
2. **New Site**: Click "New site from Git"
3. **Connect GitHub**: Authorize and select your repo
4. **Build Settings**:
   - Build command: `pnpm build`
   - Publish directory: `dist`
   - Node version: `18`
5. **Environment Variables**:
   ```
   VITE_GEMINI_API_KEY = your_api_key
   VITE_FORMSPREE_ENDPOINT = your_endpoint
   ```
6. **Deploy**: Click "Deploy site"

### Essential URLs After Deployment
- **Site URL**: `https://your-site-name.netlify.app`
- **Admin**: `https://app.netlify.com/sites/your-site-name`
- **Deploy logs**: Check for any errors

## Post-Deployment Testing

### ✅ Test These Features:
- [ ] Home page loads
- [ ] Navigation works (all links)
- [ ] Contact form submits
- [ ] AI chatbot responds
- [ ] Blog page loads with search
- [ ] Student portal login works
- [ ] Mobile responsive design
- [ ] Page refresh works (React Router)

### 🔧 Common Fixes:

**404 on page refresh?**
- ✅ Fixed by `netlify.toml` redirects

**Environment variables not working?**
- Double-check spelling in Netlify dashboard
- Ensure they start with `VITE_`
- Redeploy after adding variables

**Images not loading?**
- Check file paths start with `/`
- Verify images are in `public/` folder

## Success! 🎉

Your FAANG Tech Lab website is now live on Netlify!

**Next Steps:**
1. Test all functionality
2. Set up custom domain (optional)
3. Enable form notifications in Netlify
4. Add Google Analytics (optional)
5. Share your live site! 🚀
