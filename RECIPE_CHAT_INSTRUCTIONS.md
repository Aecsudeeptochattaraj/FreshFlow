# Recipe Chatbot - How to Run

## Prerequisites
1. Your Azure Function backend must be running at `http://localhost:7267`
2. Node.js and npm must be installed on your system

## Setup Instructions

### 1. Start Your Azure Function
Make sure your Azure function is running and accessible at:
```
http://localhost:7267/api/GetRecipeAndCart
```

### 2. Install Frontend Dependencies
Navigate to the frontend directory and install dependencies:
```bash
cd frontend
npm install
```

### 3. Start the Frontend Server
In the frontend directory, run:
```bash
npm run dev
```

### 4. Access the Recipe Chatbot
Open your browser and go to:
```
http://localhost:3000/recipe-chat
```

## Using the Chatbot

### Recipe Queries
The chatbot automatically detects recipe requests. Try these examples:
- `recipe biryani`
- `find chicken curry`
- `show me a recipe for biryani for 4 people`
- `recipe pancakes for 2 servings`

### Features
- **Smart Detection**: Automatically identifies recipe requests
- **Servings Support**: Extracts servings from queries like "recipe biryani for 4 people"
- **Formatted Display**: Shows recipes with proper formatting (title, ingredients, steps)
- **Affiliate Links**: Displays links to purchase ingredients when available

### Navigation
- Click "General Chat" to switch back to the main chat interface
- Click "Clear Chat" to reset the conversation

## Troubleshooting

### CORS Issues
If you encounter CORS errors, make sure your Azure function has CORS configured to allow requests from `http://localhost:3000`.

### Connection Refused
If you see "Connection refused" errors:
1. Verify your Azure function is running
2. Check that it's accessible at `http://localhost:7267`
3. Ensure no firewall is blocking the connection

### Recipe Not Found
If recipes aren't found:
1. Check your Azure function logs for errors
2. Verify the query format matches what your backend expects