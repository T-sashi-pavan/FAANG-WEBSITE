# 🚀 Netlify Deployment Guide for FAANG Tech Lab

This guide will help you deploy your React + Vite application to Netlify with all features working properly.

## 📋 Prerequisites

- [x] GitHub account
- [x] Netlify account (free)
- [x] Your project pushed to GitHub
- [x] Environment variables ready

## 🛠️ Step 1: Prepare Your Project

### 1.1 Create Build Configuration

Create a `netlify.toml` file in your project root:

```toml
[build]
  command = "pnpm build"
  publish = "dist"

[build.environment]
  NODE_VERSION = "18"

# Redirect all routes to index.html for SPA routing
[[redirects]]
  from = "/*"
  to = "/index.html"
  status = 200

# Headers for security and performance
[[headers]]
  for = "/*"
  [headers.values]
    X-Frame-Options = "DENY"
    X-XSS-Protection = "1; mode=block"
    X-Content-Type-Options = "nosniff"
    Referrer-Policy = "strict-origin-when-cross-origin"

[[headers]]
  for = "/assets/*"
  [headers.values]
    Cache-Control = "public, max-age=31536000, immutable"
```

### 1.2 Update Package.json Scripts

Ensure your `package.json` has the correct build script:

```json
{
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "preview": "vite preview",
    "lint": "eslint . --ext ts,tsx --report-unused-disable-directives --max-warnings 0"
  }
}
```

### 1.3 Environment Variables Setup

Create a `.env.example` file with placeholders:

```env
# Gemini AI Chatbot
VITE_GEMINI_API_KEY=your_gemini_api_key_here

# Formspree Contact Form
VITE_FORMSPREE_ENDPOINT=your_formspree_endpoint_here
```

## 🌐 Step 2: Deploy to Netlify

### Method A: Git-based Deployment (Recommended)

1. **Push to GitHub**:
   ```bash
   git add .
   git commit -m "Prepare for Netlify deployment"
   git push origin main
   ```

2. **Connect to Netlify**:
   - Go to [netlify.com](https://netlify.com)
   - Sign up/Login with GitHub
   - Click "New site from Git"
   - Choose GitHub and authorize
   - Select your repository

3. **Configure Build Settings**:
   - **Branch to deploy**: `main`
   - **Build command**: `pnpm build`
   - **Publish directory**: `dist`
   - **Node version**: `18`

4. **Add Environment Variables**:
   - Go to Site Settings > Environment Variables
   - Add your variables:
     ```
     VITE_GEMINI_API_KEY = your_actual_api_key
     VITE_FORMSPREE_ENDPOINT = your_actual_formspree_endpoint
     ```

5. **Deploy**:
   - Click "Deploy site"
   - Wait for build to complete (usually 2-3 minutes)

### Method B: Manual Deployment

1. **Build Locally**:
   ```bash
   pnpm build
   ```

2. **Deploy via Drag & Drop**:
   - Go to [netlify.com/drop](https://netlify.com/drop)
   - Drag the `dist` folder to the deployment area
   - Get your temporary URL

## ⚙️ Step 3: Configure Domain & Settings

### 3.1 Custom Domain (Optional)

1. **Add Domain**:
   - Go to Site Settings > Domain Management
   - Click "Add custom domain"
   - Enter your domain name

2. **Configure DNS**:
   - Point your domain's DNS to Netlify:
     ```
     Type: A Record
     Name: @
     Value: 75.2.60.5
     ```

### 3.2 HTTPS & Security

- ✅ Netlify automatically provides HTTPS
- ✅ SSL certificate is auto-generated
- ✅ HTTP redirects to HTTPS

### 3.3 Form Handling (Netlify Forms)

For your contact form, you can use Netlify's built-in form handling:

1. **Update Contact Form** (alternative to Formspree):
   ```html
   <form name="contact" method="POST" data-netlify="true">
     <input type="hidden" name="form-name" value="contact" />
     <!-- your form fields -->
   </form>
   ```

2. **Enable in Netlify**:
   - Go to Site Settings > Forms
   - Forms are automatically detected

## 🔧 Step 4: Optimize Performance

### 4.1 Build Optimizations

Update your `vite.config.ts`:

```typescript
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'
import path from 'path'

export default defineConfig({
  plugins: [react()],
  resolve: {
    alias: {
      "@": path.resolve(__dirname, "./src"),
    },
  },
  build: {
    rollupOptions: {
      output: {
        manualChunks: {
          vendor: ['react', 'react-dom', 'react-router-dom'],
          ui: ['lucide-react', '@radix-ui/react-dialog'],
        }
      }
    }
  }
})
```

### 4.2 Image Optimization

- Compress images before deployment
- Use WebP format when possible
- Implement lazy loading (already done in your blog)

## 🚨 Step 5: Troubleshooting

### Common Issues & Solutions

1. **404 on Refresh**:
   - ✅ Fixed by `netlify.toml` redirects

2. **Environment Variables Not Working**:
   - Ensure variables start with `VITE_`
   - Check spelling in Netlify dashboard
   - Redeploy after adding variables

3. **Build Failures**:
   ```bash
   # Check build locally first
   pnpm build
   ```

4. **Missing Dependencies**:
   ```bash
   # Clear cache and reinstall
   rm -rf node_modules pnpm-lock.yaml
   pnpm install
   ```

## 📊 Step 6: Analytics & Monitoring

### 6.1 Netlify Analytics

- Go to Site Overview > Analytics
- Enable Netlify Analytics (paid feature)

### 6.2 Google Analytics (Free)

Add to your `index.html`:

```html
<!-- Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=GA_MEASUREMENT_ID"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'GA_MEASUREMENT_ID');
</script>
```

## 🎯 Step 7: Post-Deployment Checklist

- [ ] Website loads correctly
- [ ] All routes work (React Router)
- [ ] Contact form submits successfully
- [ ] AI chatbot responds properly
- [ ] Images and assets load
- [ ] Mobile responsiveness
- [ ] HTTPS enabled
- [ ] Custom domain (if applicable)
- [ ] Analytics tracking

## 🔗 Useful Netlify Features

### Branch Previews
- Automatic preview deployments for PR branches
- Great for testing before merging

### Functions (Serverless)
- Can replace some backend functionality
- Useful for API endpoints

### Edge Functions
- Run at the edge for better performance
- Good for geo-targeting

## 📞 Support

If you encounter issues:

1. **Netlify Docs**: [docs.netlify.com](https://docs.netlify.com)
2. **Community**: [answers.netlify.com](https://answers.netlify.com)
3. **Status**: [netlifystatus.com](https://netlifystatus.com)

## 🎉 Success!

Your FAANG Tech Lab website should now be live on Netlify! 

**Sample URL**: `https://faang-tech-lab.netlify.app`

---

> 💡 **Pro Tip**: Enable branch deploys to automatically deploy feature branches for testing before merging to main!
