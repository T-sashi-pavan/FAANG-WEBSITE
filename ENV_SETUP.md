# Environment Setup Guide

## 🔧 Setting Up Environment Variables

Your `.env` file has been created in the project root directory with the following structure:

```
faang-mine/
├── .env              # Your actual environment variables (keep private)
├── .env.example      # Template file (safe to commit)
├── package.json
└── ...
```

## 🔑 Required API Keys

### 1. Google Gemini API Key

**To get your Gemini API key:**
1. Visit [Google AI Studio](https://makersuite.google.com/app/apikey)
2. Sign in with your Google account
3. Click "Create API Key"
4. Copy the generated key
5. Replace `your_gemini_api_key_here` in your `.env` file

**Example:**
```env
VITE_GEMINI_API_KEY=AIzaSyDxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```

### 2. Formspree Endpoint

**To get your Formspree endpoint:**
1. Visit [Formspree.io](https://formspree.io)
2. Sign up/login to your account
3. Create a new form
4. Copy the form endpoint URL
5. Replace `your_formspree_endpoint_here` in your `.env` file

**Example:**
```env
VITE_FORMSPREE_ENDPOINT=https://formspree.io/f/xpzgkqyv
```

## 🛡️ Security Notes

- ✅ Your `.env` file is already protected by `.gitignore`
- ✅ Never commit real API keys to version control
- ✅ Use `.env.example` as a template for team members
- ✅ Prefix environment variables with `VITE_` for client-side access

## 🚀 After Setup

1. **Restart your development server** after adding environment variables:
   ```bash
   pnpm dev
   ```

2. **Test the AI chatbot** - it will automatically switch from mock responses to real Gemini API responses

3. **Test the contact form** - submissions will be sent to your Formspree endpoint

## 🔄 Development vs Production

- **Development**: Use `.env` file locally
- **Production**: Set environment variables in your hosting platform:
  - Vercel: Project Settings → Environment Variables
  - Netlify: Site Settings → Environment Variables
  - Other platforms: Check their documentation

## 📝 Environment Variables Reference

| Variable | Purpose | Required |
|----------|---------|----------|
| `VITE_GEMINI_API_KEY` | AI chatbot functionality | Yes |
| `VITE_FORMSPREE_ENDPOINT` | Contact form submissions | Yes |
| `VITE_APP_NAME` | Application name | No |
| `VITE_APP_VERSION` | Application version | No |
| `NODE_ENV` | Environment mode | No |
