# Frontend Documentation

## Pages

### index.js
The main chatbot interface that connects to the LangChain-powered backend for general conversation.

### recipes.js
A specialized recipe finder interface that allows users to search for recipes by name and adjust serving sizes.

## API Routes

### /api/chat.js
Proxy endpoint for the general chatbot functionality.

### /api/recipes.js
Proxy endpoint for the recipe finder functionality.

## Components

### Recipe Chat Interface
- Dedicated UI for recipe searches
- Serving size adjustment
- Formatted recipe display with ingredients and steps
- Affiliate link integration for ingredient purchasing

## Styling
- Tailwind CSS for responsive design
- Custom markdown styling for recipe display
- Mobile-friendly layout

## Environment Variables
- `NEXT_PUBLIC_BACKEND_URL`: The URL of the backend server