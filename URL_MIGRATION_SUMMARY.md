# URL Centralization Migration Summary

## ✅ **Migration Complete**

Your project now uses a centralized URL configuration system! All URLs are now defined in a single location, making deployment and maintenance much easier.

## 🔄 **What Changed**

### Files Created:
- ✅ `config/urls.js` - Centralized URL configuration
- ✅ `env.example` - Environment variables template
- ✅ `CONFIGURATION.md` - Comprehensive configuration guide
- ✅ `scripts/update-urls.js` - URL update utility
- ✅ `scripts/show-config.js` - Configuration display utility
- ✅ `URL_MIGRATION_SUMMARY.md` - This summary document

### Files Updated:
- ✅ `pages/api/chat.js` - Now uses `getAzureFunctionUrl()` instead of hardcoded URL
- ✅ `package.json` - Added utility scripts and module type
- ✅ `test-frontend.js` - Updated with note about centralized config

## 🚀 **How to Use**

### 1. **View Current Configuration**
```bash
npm run config:show
```

### 2. **Update Production URLs**
```bash
npm run update-urls:prod https://your-production-domain.com
```

### 3. **Update Staging URLs**
```bash
npm run update-urls:staging https://your-staging-domain.com
```

### 4. **Use in Code**
```javascript
import { getAzureFunctionUrl, getFrontendUrl } from '../config/urls';

// Instead of hardcoded URLs
const response = await axios.post(getAzureFunctionUrl(), data);
```

## 🎯 **Benefits Achieved**

1. **Single Source of Truth** - All URLs defined in one place
2. **Easy Deployment** - Change URLs once for all environments
3. **Environment Detection** - Automatic switching between dev/prod
4. **Type Safety** - Consistent URL structure across the app
5. **Maintenance** - Easy to update URLs across the entire project

## 🔧 **Environment Variables**

Create a `.env` file based on `env.example`:

```bash
# Frontend URL (public - accessible from client-side)
NEXT_PUBLIC_FRONTEND_URL=http://localhost:3000

# Backend URL (server-side only)
BACKEND_URL=http://localhost:7267

# Azure Function URL (server-side only)
AZURE_FUNCTION_URL=http://localhost:7267/api/GetRecipeAndCart

# Development/Production Mode
NODE_ENV=development
```

## 📋 **Before vs After**

### Before (Hardcoded):
```javascript
const response = await axios.post('http://localhost:7267/api/GetRecipeAndCart', data);
```

### After (Centralized):
```javascript
import { getAzureFunctionUrl } from '../../config/urls';
const response = await axios.post(getAzureFunctionUrl(), data);
```

## 🛠️ **Adding New URLs**

To add a new URL to the system:

1. **Add to config/urls.js**:
```javascript
development: {
  // ... existing URLs
  newService: 'http://localhost:8080/api/new-service'
},
production: {
  // ... existing URLs
  newService: process.env.NEW_SERVICE_URL || 'https://your-new-service.com/api'
}
```

2. **Export a getter**:
```javascript
export const getNewServiceUrl = () => getUrls().newService;
```

3. **Use in code**:
```javascript
import { getNewServiceUrl } from '../config/urls';
const response = await fetch(getNewServiceUrl());
```

## 🔍 **Environment Detection**

The system automatically detects the environment:
- **Client-side**: Checks `window.location.hostname`
- **Server-side**: Uses `process.env.NODE_ENV`
- **Development**: Uses `localhost` URLs
- **Production**: Uses environment variables or fallback URLs

## 📚 **Documentation**

- **`CONFIGURATION.md`** - Complete configuration guide
- **`env.example`** - Environment variables template
- **`config/urls.js`** - Main configuration file with comments

## ✅ **Verification**

The migration has been tested and verified:
- ✅ Build successful (`npm run build`)
- ✅ Configuration script working (`npm run config:show`)
- ✅ API routes using centralized URLs
- ✅ All functionality preserved

## 🎉 **Next Steps**

1. **Set up environment variables** for your deployment
2. **Update production URLs** using the utility scripts
3. **Test in your deployment environment**
4. **Update documentation** with your actual URLs

Your project is now ready for easy deployment and maintenance! 🚀
