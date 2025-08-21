# Recipe Price Comparison & GenAI Fallback System

This document describes the implementation of a comprehensive recipe price comparison system with GenAI fallback functionality when the Azure Function fails.

## 🚀 Features Implemented

### 1. GenAI Fallback System
- **Automatic Fallback**: When Azure Function fails or returns no response, the system automatically falls back to GenAI
- **Structured Output**: GenAI generates recipe data in the same format as Azure Function output
- **JSON Response**: GenAI returns structured JSON with recipe title, ingredients, steps, and metadata
- **Error Handling**: Graceful handling of parsing errors with fallback to raw response

### 2. Live Price Comparison
- **Multi-Platform Support**: Pricing from Zepto, Blinkit, Swiggy Instamart, and Amazon Fresh
- **Real-time Simulation**: Simulates live API calls with price variations and delays
- **Fallback Pricing**: Comprehensive fallback database for common ingredients
- **Concurrent Fetching**: Parallel API calls for optimal performance

### 3. Smart Cost Analysis
- **Total Cost Calculation**: Automatic calculation of total recipe cost per platform
- **Best Deal Detection**: Highlights the platform with the lowest total price
- **Availability Tracking**: Shows which ingredients are available on each platform
- **Price Variations**: Simulates real market price fluctuations

### 4. Modern UI Components
- **Price Comparison Table**: Clear comparison of ingredient prices across platforms
- **Cost Summary Cards**: Visual representation of total costs with best deal highlighting
- **Shopping Links**: Direct links to each platform with availability status
- **Loading States**: Smooth loading animations and error handling

## 📁 File Structure

```
frontend/
├── components/
│   ├── PriceComparison.js          # Main price comparison component
│   └── RecipeDisplay.js            # Updated with price comparison
├── pages/
│   ├── api/
│   │   ├── chat.js                 # Updated with GenAI fallback
│   │   └── pricing.js              # New pricing API endpoint
│   └── test-pricing.js             # Demo page for testing
├── utils/
│   ├── priceComparison.js          # Price comparison utilities
│   └── affiliateLinks.js           # Existing affiliate functionality
└── README_PRICE_COMPARISON.md      # This documentation
```

## 🔧 Technical Implementation

### GenAI Fallback (pages/api/chat.js)

```javascript
// When Azure Function fails, GenAI generates structured recipe
const prompt = `Please provide a complete recipe in the following JSON format:
{
  "recipe_title": "Recipe Name",
  "requested_servings": ${servings},
  "ingredients": [
    {"Name": "Ingredient 1", "Quantity": "amount", "Unit": "unit"}
  ],
  "steps": ["Step 1 description"],
  "cooking_time": "estimated time",
  "difficulty": "easy/medium/hard",
  "cuisine": "cuisine type"
}`;
```

### Price Comparison Service (utils/priceComparison.js)

```javascript
// Simulates live API calls with fallback data
async function fetchLivePricing(ingredientName, platform) {
  // Simulate API delay and potential failures
  await new Promise(resolve => setTimeout(resolve, Math.random() * 1000 + 500));
  
  // Add price variations to simulate live data
  const variation = (Math.random() - 0.5) * 0.1; // ±5% variation
  const livePrice = Math.round(basePrice * (1 + variation));
  
  return { price: livePrice, unit: 'kg', available: true };
}
```

### Price Comparison Component (components/PriceComparison.js)

```javascript
// Fetches pricing data and displays comparison
const fetchPricing = async () => {
  const response = await axios.post('/api/pricing', { ingredients });
  setPricingData(response.data.pricing);
  setCosts(response.data.costs);
};
```

## 🛠️ API Endpoints

### POST /api/pricing
Fetches pricing data for a list of ingredients.

**Request:**
```json
{
  "ingredients": [
    {"name": "basmati rice", "quantity": "2", "unit": "cups"},
    {"name": "chicken", "quantity": "500", "unit": "g"}
  ]
}
```

**Response:**
```json
{
  "success": true,
  "pricing": {
    "basmati rice": {
      "pricing": {
        "zepto": {"price": 120, "unit": "kg", "available": true},
        "blinkit": {"price": 115, "unit": "kg", "available": true}
      }
    }
  },
  "costs": {
    "platformTotals": {
      "zepto": {"total": 450, "available": 5, "unavailable": 0}
    },
    "bestDeal": "zepto",
    "lowestPrice": 450
  }
}
```

## 🎯 Usage Examples

### Testing the System

1. **Visit the demo page**: Navigate to `/test-pricing` to see the price comparison in action
2. **Test GenAI fallback**: Disconnect Azure Function to trigger GenAI fallback
3. **View price variations**: Refresh the page to see simulated price changes

### Integration with Existing Chatbot

The price comparison automatically appears when a recipe is displayed:

```javascript
// In RecipeDisplay component
<PriceComparison 
  ingredients={cleanedIngredients}
  recipeTitle={recipeData.recipe_title}
/>
```

## 🔄 Data Flow

1. **User requests recipe** → Chat API called
2. **Azure Function attempt** → If fails, GenAI fallback triggered
3. **Recipe data received** → RecipeDisplay component renders
4. **Price comparison triggered** → Pricing API called for all ingredients
5. **Live pricing fetched** → PriceComparison component displays results
6. **Best deal calculated** → Platform with lowest total cost highlighted

## 🎨 UI Features

### Price Comparison Table
- Grid layout showing ingredient prices across platforms
- Color-coded availability status
- Unit information for each price

### Cost Summary Cards
- Total cost per platform
- Best deal highlighting with green border
- Availability count for each platform

### Shopping Links
- Direct links to each platform
- Disabled state for platforms with no available items
- Visual indicators for platform status

## 🔧 Configuration

### Environment Variables
```bash
GROQ_API_KEY=your_groq_api_key
AMAZON_AFFILIATE_TAG=your_amazon_tag
```

### Platform Configuration
Platform settings can be modified in `utils/priceComparison.js`:

```javascript
const PLATFORMS = {
  zepto: {
    name: 'Zepto',
    color: '#FF6B35',
    icon: '⚡',
    baseUrl: 'https://www.zepto.in'
  }
  // ... other platforms
};
```

## 🚀 Future Enhancements

### Real API Integration
- Replace simulation with actual platform APIs
- Implement web scraping for real-time pricing
- Add caching for improved performance

### Advanced Features
- Price history tracking
- Price alerts for specific ingredients
- Recipe cost optimization suggestions
- Nutritional information integration

### Platform Expansion
- Add more grocery platforms
- Support for international markets
- Restaurant delivery integration

## 🐛 Troubleshooting

### Common Issues

1. **GenAI not responding**: Check GROQ_API_KEY environment variable
2. **Pricing not loading**: Verify network connectivity and API endpoints
3. **JSON parsing errors**: GenAI response format issues, check console logs

### Debug Mode
Enable detailed logging by setting:
```javascript
console.log('GenAI fallback response:', aiResponse);
console.log('Pricing data:', response.data);
```

## 📊 Performance Considerations

- **Concurrent API calls**: All platform pricing fetched simultaneously
- **Error isolation**: Individual platform failures don't affect others
- **Caching potential**: Ready for Redis/Memcached integration
- **Lazy loading**: Price comparison loads after recipe display

## 🔒 Security Considerations

- **API key protection**: Environment variables for sensitive data
- **Input validation**: Sanitized ingredient names
- **Error handling**: No sensitive data exposed in error messages
- **Rate limiting**: Ready for implementation with actual APIs

This implementation provides a robust, scalable foundation for recipe price comparison with intelligent fallback mechanisms and a modern, user-friendly interface.
