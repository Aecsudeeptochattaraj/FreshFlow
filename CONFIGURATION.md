# Configuration Guide

This project now uses a centralized URL configuration system for easier maintenance and deployment.

## 📁 Configuration Files

### `config/urls.js`
The main configuration file containing all URLs used throughout the project.

### `env.example`
Example environment variables file. Copy to `.env` and update values.

## 🔧 How to Configure URLs

### 1. Development Environment
URLs are automatically detected based on the environment:
- **Development**: Uses `localhost` URLs
- **Production**: Uses environment variables or fallback URLs

### 2. Environment Variables
Set these in your `.env` file:

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

### 3. Production Configuration
For production deployment, update the URLs in `config/urls.js`:

```javascript
production: {
  frontend: 'https://your-production-domain.com',
  backend: 'https://your-backend-domain.com',
  azureFunction: 'https://your-azure-function-url.com/api/GetRecipeAndCart'
}
```

## 🚀 Usage Examples

### In API Routes
```javascript
import { getAzureFunctionUrl } from '../../config/urls';

const response = await axios.post(getAzureFunctionUrl(), {
  Query: query,
  Servings: servings
});
```

### In Components
```javascript
import { getFrontendUrl } from '../config/urls';

const frontendUrl = getFrontendUrl();
```

### Get All Current URLs
```javascript
import { currentUrls } from '../config/urls';

console.log('Current URLs:', currentUrls);
```

## 🔄 Migration Guide

### Before (Hardcoded URLs)
```javascript
const response = await axios.post('http://localhost:7267/api/GetRecipeAndCart', data);
```

### After (Centralized Configuration)
```javascript
import { getAzureFunctionUrl } from '../../config/urls';
const response = await axios.post(getAzureFunctionUrl(), data);
```

## 📋 Files Updated

The following files have been updated to use centralized configuration:

- ✅ `pages/api/chat.js` - Azure Function URL
- ✅ `config/urls.js` - Centralized configuration
- ✅ `env.example` - Environment variables example
- ✅ `test-frontend.js` - Updated with note about centralized config

## 🎯 Benefits

1. **Single Source of Truth**: All URLs defined in one place
2. **Easy Deployment**: Change URLs once for all environments
3. **Environment Detection**: Automatic switching between dev/prod
4. **Type Safety**: Consistent URL structure across the app
5. **Maintenance**: Easy to update URLs across the entire project

## 🔍 Environment Detection

The system automatically detects the environment:

- **Client-side**: Checks `window.location.hostname`
- **Server-side**: Uses `process.env.NODE_ENV`
- **Development**: Uses `localhost` URLs
- **Production**: Uses environment variables or fallback URLs

## 🛠️ Adding New URLs

To add a new URL to the centralized system:

1. Add it to `config/urls.js`:
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

2. Export a getter function:
```javascript
export const getNewServiceUrl = () => getUrls().newService;
```

3. Use it in your code:
```javascript
import { getNewServiceUrl } from '../config/urls';
const response = await fetch(getNewServiceUrl());
```

## 📝 Notes

- Environment variables prefixed with `NEXT_PUBLIC_` are accessible on the client-side
- Server-side only variables should not have the `NEXT_PUBLIC_` prefix
- The system falls back to development URLs if environment detection fails
- Always use the getter functions instead of accessing the config directly
