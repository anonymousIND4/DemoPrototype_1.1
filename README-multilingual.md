# AgroAI Multilingual Support Implementation

## Overview

This document explains how multilingual support has been implemented in the AgroAI website using both local translations and the LibreTranslate API for dynamic translation capabilities.

## Implementation Details

### 1. Local Translations

The website uses a local translation system defined in `language.js` that contains predefined translations for:
- English (en)
- Hindi (hi)
- Tamil (ta)
- Telugu (te)

These translations are stored in a JavaScript object and applied to HTML elements with `data-i18n` attributes.

### 2. LibreTranslate API Integration

For languages not available in the local translations or for dynamic content, the website now integrates with LibreTranslate, a free and open-source machine translation API.

#### Key Features:

- **On-demand Translation**: Translates content using the API when local translations aren't available
- **Auto-Translate Button**: Added to the language dropdown for one-click translation of the entire page
- **Loading Indicator**: Shows a visual indicator during translation process
- **Fallback Mechanism**: Uses local translations when available for better performance

## Files Added/Modified

1. **New File: `js/translate-api.js`**
   - Contains the LibreTranslate API integration
   - Provides functions for translating text and entire pages
   - Adds UI elements for translation functionality

2. **Modified: `js/language.js`**
   - Updated to work with the API translation system
   - Added conditional logic to use API translation when local translations aren't available

3. **Modified: All HTML files**
   - Added the `translate-api.js` script to all pages

## How to Use

### For Users

1. Click on the language selector in the navigation bar
2. Select your desired language from the dropdown
3. If the language is available in local translations, it will be applied immediately
4. For other languages or to force translation, click the "Auto-Translate" button

### For Developers

#### Adding New Local Translations

To add a new language to the local translations:

1. Open `js/language.js`
2. Add a new language object to the `translations` object
3. Provide translations for all keys

```javascript
'fr': {
    'nav_home': 'Accueil',
    'nav_about': 'À propos',
    // Add all other translation keys
}
```

#### Changing the Translation API

The current implementation uses the public LibreTranslate instance at `https://libretranslate.de/translate`. To use a different instance or API:

1. Open `js/translate-api.js`
2. Modify the `LIBRETRANSLATE_API_URL` constant
3. Update the request parameters in the `translateText()` function if needed

## API Usage Notes

- The current implementation uses public LibreTranslate instances which may have rate limits
- For production use with high traffic, consider:
  - Self-hosting LibreTranslate
  - Using a paid API service with higher limits
  - Implementing caching for translated content

## Testing

A test page has been created at `test-translate.html` that allows direct testing of the translation API functionality.