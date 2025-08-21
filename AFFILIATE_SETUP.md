# Affiliate Link Setup Guide

This guide explains how to set up affiliate tracking for the AI Recipe & Quick Commerce Ordering Agent.

## Environment Variables

Create a `.env.local` file in your project root with the following variables:

```bash
# API Keys
GROQ_API_KEY=your_groq_api_key_here
PINECONE_API_KEY=your_pinecone_api_key_here
PINECONE_ENVIRONMENT=your_pinecone_environment_here

# Affiliate Tracking
AMAZON_AFFILIATE_TAG=your-tag-21

# Azure Function (if using)
AZURE_FUNCTION_URL=http://localhost:7267/api/GetRecipeAndCart

# Google Analytics (optional)
NEXT_PUBLIC_GA_ID=G-XXXXXXXXXX
```

## Affiliate Program Setup

### 1. Amazon Associates Program

1. **Sign up**: Go to [Amazon Associates India](https://affiliate-program.amazon.in/)
2. **Get your tag**: You'll receive a tracking ID like `yourtag-21`
3. **Add to environment**: Set `AMAZON_AFFILIATE_TAG=your-tag-21` in `.env.local`

### 2. Blinkit & Swiggy Instamart

These platforms don't offer public affiliate programs yet. You can:

1. **Contact them directly** for partnership opportunities
2. **Use UTM tracking** for analytics (already implemented)
3. **Track conversions** through your own analytics

## SKU Mapping

The system includes a built-in SKU mapping database in `utils/affiliateLinks.js`. To add more ingredients:

```javascript
const SKU_MAPPING = {
  'ingredient name': {
    amazon: 'AMAZON_SKU',
    blinkit: 'BLINKIT_SKU',
    swiggy: 'SWIGGY_SKU'
  }
};
```

## How Affiliate Links Work

### Amazon Fresh
- Format: `https://www.amazon.in/dp/SKU?tag=your-tag-21`
- Commission: Earn on each purchase through your link
- Tracking: Automatic through Amazon Associates

### Blinkit & Swiggy
- Format: `https://platform.com/cart?items=SKU1,SKU2&utm_source=recipe-ai`
- Tracking: UTM parameters for analytics
- Commission: Requires direct partnership

## Testing Affiliate Links

1. **Start the development server**: `npm run dev`
2. **Ask for a recipe**: "I want to cook chicken biryani for 2 people"
3. **Check affiliate links**: Look for the "Order Ingredients Online" section
4. **Test links**: Click on platform buttons to verify they work

## Analytics Setup

### Google Analytics (Optional)

1. **Create GA4 property** in Google Analytics
2. **Get measurement ID**: Format `G-XXXXXXXXXX`
3. **Add to environment**: `NEXT_PUBLIC_GA_ID=G-XXXXXXXXXX`
4. **Track events**: Affiliate link clicks are automatically tracked

### Custom Analytics

The system tracks:
- Affiliate link clicks
- Platform preferences
- Recipe requests
- Conversion events

## Revenue Optimization

### Best Practices

1. **Multiple platforms**: Offer links to all available platforms
2. **Clear disclosure**: Always mention affiliate relationships
3. **Quality content**: Focus on helpful recipe content
4. **Mobile optimization**: Ensure links work on mobile devices

### Commission Rates

- **Amazon**: 1-10% depending on category
- **Blinkit**: Varies by partnership
- **Swiggy**: Varies by partnership

## Troubleshooting

### Common Issues

1. **Links not working**: Check SKU mapping in `utils/affiliateLinks.js`
2. **No affiliate tag**: Verify `AMAZON_AFFILIATE_TAG` in environment
3. **Missing ingredients**: Add new ingredients to SKU mapping
4. **Analytics not tracking**: Check Google Analytics setup

### Debug Mode

Enable debug logging by adding to your environment:

```bash
DEBUG_AFFILIATE=true
```

## Legal Compliance

1. **Disclosure**: Always disclose affiliate relationships
2. **Privacy**: Follow GDPR and local privacy laws
3. **Terms**: Comply with each platform's affiliate terms
4. **Taxes**: Report affiliate income for tax purposes

## Support

For issues with:
- **Amazon Associates**: Contact Amazon support
- **Blinkit/Swiggy**: Reach out to their business teams
- **Technical issues**: Check the troubleshooting section above
