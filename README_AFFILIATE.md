# AI Recipe & Quick Commerce Ordering Agent

A Next.js application that generates recipes and provides affiliate links for ordering ingredients from quick commerce platforms.

## Features

- 🤖 **AI Recipe Generation**: Uses Groq AI to generate recipes based on user requests
- 🛒 **Affiliate Links**: Automatically generates affiliate links for Blinkit, Swiggy Instamart, and Amazon Fresh
- 📱 **Modern UI**: Beautiful, responsive interface with Tailwind CSS
- 🔗 **SKU Mapping**: Intelligent ingredient-to-SKU mapping system
- 📊 **Analytics**: Built-in tracking for affiliate link clicks
- 🎯 **Commission Tracking**: Earn money through affiliate partnerships

## Quick Start

1. **Clone and install dependencies**:
   ```bash
   npm install
   ```

2. **Set up environment variables**:
   Create a `.env.local` file:
   ```bash
   GROQ_API_KEY=your_groq_api_key
   PINECONE_API_KEY=your_pinecone_api_key
   PINECONE_ENVIRONMENT=your_pinecone_env
   AMAZON_AFFILIATE_TAG=your-tag-21
   ```

3. **Start the development server**:
   ```bash
   npm run dev
   ```

4. **Test the application**:
   - Visit `http://localhost:3000`
   - Ask for a recipe: "I want to cook chicken biryani for 2 people"
   - See affiliate links generated automatically

## How Affiliate Links Work

### 1. Recipe Request
User asks for a recipe with serving size:
```
"I want to cook chicken biryani for 2 people"
```

### 2. AI Processing
- AI generates recipe with ingredients and quantities
- System maps ingredients to platform SKUs
- Affiliate links are created for each platform

### 3. Affiliate Link Generation

#### Amazon Fresh
```
https://www.amazon.in/dp/B07XYZ1234?tag=your-tag-21&linkCode=ogi&language=en_IN
```

#### Blinkit
```
https://blinkit.com/cart?items=SKU12345,SKU67890&utm_source=recipe-ai&utm_medium=affiliate&utm_campaign=recipe-ordering
```

#### Swiggy Instamart
```
https://www.swiggy.com/cart?items=SKU12345,SKU67890&utm_source=recipe-ai&utm_medium=affiliate&utm_campaign=recipe-ordering
```

### 4. User Experience
- User sees recipe with ingredients
- Clicks on platform buttons to order
- Gets redirected to pre-filled cart
- You earn commission on purchases

## File Structure

```
frontend/
├── components/
│   ├── AffiliateLinks.js      # Affiliate link display component
│   ├── RecipeDisplay.js       # Recipe display with ingredients
│   └── AffiliateTest.js       # Test component for demo
├── utils/
│   └── affiliateLinks.js      # Affiliate link generation utilities
├── pages/
│   ├── index.js              # Main chat interface
│   ├── api/chat.js           # API endpoint for recipe generation
│   └── test-affiliate.js     # Test page for affiliate functionality
└── AFFILIATE_SETUP.md        # Detailed setup guide
```

## Key Components

### AffiliateLinks Component
- Displays affiliate links in an attractive format
- Handles click tracking
- Opens links in new tabs
- Shows platform icons and descriptions

### RecipeDisplay Component
- Shows recipe title, ingredients, and steps
- Integrates affiliate links
- Provides cooking tips
- Responsive design

### affiliateLinks Utility
- SKU mapping database
- Link generation functions
- Platform-specific formatting
- Error handling

## SKU Mapping System

The system includes a comprehensive SKU mapping database:

```javascript
const SKU_MAPPING = {
  'basmati rice': {
    amazon: 'B07XYZ1234',
    blinkit: 'SKU_RICE_001',
    swiggy: 'SWIGGY_RICE_001'
  },
  'chicken': {
    amazon: 'B07XYZ1236',
    blinkit: 'SKU_CHICKEN_001',
    swiggy: 'SWIGGY_CHICKEN_001'
  }
  // ... more ingredients
};
```

## Affiliate Program Setup

### Amazon Associates
1. Sign up at [Amazon Associates India](https://affiliate-program.amazon.in/)
2. Get your tracking tag (e.g., `yourtag-21`)
3. Add to environment: `AMAZON_AFFILIATE_TAG=your-tag-21`

### Blinkit & Swiggy
- Contact their business teams for partnership opportunities
- Use UTM tracking for analytics
- Implement custom tracking solutions

## Testing

### Test Affiliate Links
Visit `/test-affiliate` to see a demo of the affiliate link functionality with sample data.

### Test Recipe Generation
1. Start the app: `npm run dev`
2. Ask for recipes like:
   - "I want to cook chicken biryani for 2 people"
   - "Make me a pasta recipe for 4 servings"
   - "Vegetarian curry for 3 people"

## Revenue Optimization

### Best Practices
1. **Multiple platforms**: Offer all available options
2. **Clear disclosure**: Always mention affiliate relationships
3. **Quality content**: Focus on helpful recipe content
4. **Mobile optimization**: Ensure links work on all devices

### Commission Rates
- **Amazon**: 1-10% depending on category
- **Blinkit**: Varies by partnership
- **Swiggy**: Varies by partnership

## Analytics & Tracking

### Google Analytics
Add your GA4 measurement ID:
```bash
NEXT_PUBLIC_GA_ID=G-XXXXXXXXXX
```

### Custom Events
The system tracks:
- Affiliate link clicks
- Platform preferences
- Recipe requests
- Conversion events

## Legal Compliance

1. **Disclosure**: Always disclose affiliate relationships
2. **Privacy**: Follow GDPR and local privacy laws
3. **Terms**: Comply with each platform's affiliate terms
4. **Taxes**: Report affiliate income for tax purposes

## Troubleshooting

### Common Issues

1. **Links not working**
   - Check SKU mapping in `utils/affiliateLinks.js`
   - Verify affiliate tags in environment variables

2. **No affiliate links showing**
   - Ensure ingredients are in the SKU mapping
   - Check console for errors

3. **Analytics not tracking**
   - Verify Google Analytics setup
   - Check browser console for errors

### Debug Mode
Add to environment:
```bash
DEBUG_AFFILIATE=true
```

## Contributing

1. Fork the repository
2. Create a feature branch
3. Add new ingredients to SKU mapping
4. Test affiliate link generation
5. Submit a pull request

## Support

- **Technical issues**: Check troubleshooting section
- **Amazon Associates**: Contact Amazon support
- **Blinkit/Swiggy**: Reach out to their business teams

## License

This project is licensed under the MIT License.

---

**Note**: This is a demonstration of affiliate link integration. For production use, ensure compliance with all platform terms and local regulations.
