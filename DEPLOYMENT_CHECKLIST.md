# 🚀 Deployment Checklist

## ✅ **Pre-Deployment Steps**

### 1. **Project Preparation**
- [x] Build successful (`npm run build`)
- [x] All tests passing
- [x] Configuration files ready
- [x] Environment variables documented

### 2. **Code Review**
- [x] No hardcoded localhost URLs
- [x] All imports using centralized config
- [x] Error handling in place
- [x] Performance optimized

## 🔧 **Deployment Steps**

### **Step 1: Install Vercel CLI**
```bash
npm install -g vercel
```

### **Step 2: Deploy to Vercel**
```bash
vercel
```

**Follow the prompts:**
- [ ] Link to existing project or create new
- [ ] Set project name (e.g., "recipe-assistant")
- [ ] Confirm deployment settings
- [ ] Wait for deployment to complete

### **Step 3: Get Your Deployment URL**
After deployment, you'll get a URL like:
`https://your-project.vercel.app`

### **Step 4: Update Production URLs**
```bash
npm run update-urls:prod https://your-project.vercel.app
```

### **Step 5: Configure Environment Variables**
In Vercel Dashboard:
1. Go to your project
2. Settings → Environment Variables
3. Add these variables:

```bash
# Frontend URL (public)
NEXT_PUBLIC_FRONTEND_URL=https://your-project.vercel.app

# Backend URLs (server-side only)
BACKEND_URL=https://your-backend-domain.com
AZURE_FUNCTION_URL=https://your-azure-function-url.com/api/GetRecipeAndCart

# AI Service Keys
GROQ_API_KEY=your_groq_api_key_here
PINECONE_API_KEY=your_pinecone_api_key_here
PINECONE_ENVIRONMENT=your_pinecone_environment_here

# Environment
NODE_ENV=production
```

### **Step 6: Redeploy with Environment Variables**
```bash
vercel --prod
```

## 🧪 **Post-Deployment Testing**

### **Test All Features**
- [ ] Main page loads correctly
- [ ] Recipe search works
- [ ] GenAI fallback functions
- [ ] Price comparison displays
- [ ] API endpoints respond
- [ ] Mobile responsiveness

### **Check Configuration**
```bash
npm run config:show
```

### **Monitor Performance**
- [ ] Page load times
- [ ] API response times
- [ ] Error rates

## 🔗 **Custom Domain (Optional)**

### **Add Custom Domain**
1. Go to Vercel Dashboard
2. Project Settings → Domains
3. Add your custom domain
4. Update DNS records
5. Update production URLs:
```bash
npm run update-urls:prod https://your-custom-domain.com
```

## 📊 **Monitoring Setup**

### **Add Analytics**
```bash
npm install @vercel/analytics
```

### **Configure Monitoring**
- Set up error tracking
- Monitor API performance
- Track user interactions

## 🎯 **Success Criteria**

- [ ] Application accessible at production URL
- [ ] All features working correctly
- [ ] Environment variables configured
- [ ] Performance acceptable
- [ ] Error handling working
- [ ] Mobile responsive

## 🚨 **Troubleshooting**

### **Common Issues:**
1. **Environment Variables Not Working**
   - Check variable names
   - Ensure `NEXT_PUBLIC_` prefix for client-side

2. **API Endpoints Failing**
   - Verify backend URLs
   - Check CORS settings

3. **Build Failures**
   - Check for missing dependencies
   - Verify import paths

## 📞 **Support**

If you encounter issues:
1. Check Vercel deployment logs
2. Review environment variables
3. Test locally with production settings
4. Check browser console for errors

---

**Ready to deploy! Follow the steps above.** 🚀
