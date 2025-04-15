# Klaviyo-Webflow Integration

A powerful, flexible, and modular integration between Webflow forms and Klaviyo, with versioning support and robust error handling.

## Features

- **Multi-Account Support**: Connect multiple Klaviyo accounts on a single page
- **Versioned API**: Support for different Klaviyo API versions
- **Custom Field Mapping**: Map Webflow form fields to any Klaviyo fields
- **SMS Support**: Collect and validate phone numbers for SMS subscriptions
- **Event Tracking**: Track form views and submissions in Klaviyo
- **Error Handling**: Robust error handling with helpful user feedback
- **Developer-Friendly**: Modular architecture for easy maintenance
- **Webflow Compatible**: Works with all Webflow forms

## Quick Start

### 1. Add the script to your site

Add the following script to your site's head section:

```html
<script src="https://cdn.example.com/klaviyo-webflow/klaviyo-webflow.min.js"></script>
```

### 2. Initialize with your Klaviyo account

Add this script after the one above:

```html
<script>
  window.initKlaviyoWebflow({
    publicApiKey: 'YOUR_KLAVIYO_PUBLIC_API_KEY'
  });
</script>
```

Replace `YOUR_KLAVIYO_PUBLIC_API_KEY` with your Klaviyo public API key.

### 3. Configure your Webflow forms

Add the `data-klaviyo-form` attribute to any form you want to connect to Klaviyo:

```html
<form data-klaviyo-form data-klaviyo-list-id="YOUR_LIST_ID">
  <!-- Form fields -->
</form>
```

Replace `YOUR_LIST_ID` with your Klaviyo list ID.

## Form Configuration Options

Forms can be configured using data attributes or JavaScript.

### Using Data Attributes

```html
<form 
  data-klaviyo-form
  data-klaviyo-list-id="YOUR_LIST_ID"
  data-klaviyo-account-id="YOUR_PUBLIC_API_KEY"
  data-klaviyo-source="Homepage Form"
  data-klaviyo-api-version="2025-04-15"
>
  <!-- Form fields -->
</form>
```

### Using JavaScript

```javascript
window.initKlaviyoWebflow({
  publicApiKey: 'DEFAULT_PUBLIC_API_KEY',
  defaultConfig: {
    listId: 'DEFAULT_LIST_ID',
    tracking: {
      viewForm: true,
      submitForm: true
    },
    useLibPhoneNumber: true,
    debug: false
  },
  forms: {
    'contact-form': {
      listId: 'SPECIFIC_LIST_ID',
      publicApiKey: 'SPECIFIC_PUBLIC_API_KEY',
      customProperties: {
        source: 'Contact Page',
        campaign: 'Spring 2023'
      }
    }
  }
});
```

## Field Mapping

The integration automatically maps common field names to Klaviyo properties:

| Webflow Field Name | Klaviyo Property |
|-------------------|-----------------|
| email            | email           |
| name             | first_name      |
| first-name       | first_name      |
| last-name        | last_name       |
| phone            | phone_number    |
| phone-number     | phone_number    |
| company          | organization    |
| address1         | location.address1 |
| city             | location.city   |
| country          | location.country |
| region           | location.region |
| zip              | location.zip    |

### Custom Field Mapping

For custom fields, use the `data-klaviyo-field` attribute:

```html
<input type="text" name="industry" data-klaviyo-field="properties.industry">
```

Or configure mapping in JavaScript:

```javascript
window.initKlaviyoWebflow({
  // ... other config ...
  defaultConfig: {
    fieldMapping: {
      'industry': 'properties.industry',
      'job-title': 'title'
    }
  }
});
```

## Advanced Usage

### SMS Subscriptions

For SMS subscriptions, include a phone field and the script will automatically subscribe the user to SMS marketing:

```html
<form data-klaviyo-form data-klaviyo-list-id="YOUR_LIST_ID">
  <input type="email" name="email">
  <input type="tel" name="phone">
  <button type="submit">Subscribe</button>
</form>
```

To explicitly control which channels a user subscribes to, use consent fields:

```html
<input type="hidden" name="email_marketing_consent" value="true">
<input type="hidden" name="sms_marketing_consent" value="true">
```

### Version-Specific Features

To use a specific API version:

```html
<form data-klaviyo-form data-klaviyo-api-version="2025-04-15">
  <!-- Form fields -->
</form>
```

Or in JavaScript:

```javascript
window.initKlaviyoWebflow({
  // ... other config ...
  defaultConfig: {
    apiVersion: '2025-04-15'
  }
});
```

### Debugging

Enable debug mode to log detailed information to the console:

```javascript
window.initKlaviyoWebflow({
  // ... other config ...
  defaultConfig: {
    debug: true
  }
});
```

You can also use the global debug helper:

```javascript
console.log(window.klaviyoWebflowDebug());
```

## Event Handling

The integration fires custom events that you can listen for:

```javascript
document.addEventListener('klaviyoSubmitSuccess', function(event) {
  console.log('Form submitted successfully!', event.detail);
});

document.addEventListener('klaviyoSubmitError', function(event) {
  console.error('Error submitting form:', event.detail.error);
});
```

## Browser Compatibility

The integration is compatible with all modern browsers:

- Chrome 60+
- Firefox 60+
- Safari 10+
- Edge 16+
- Opera 50+

## Development

### Building from source

```
git clone https://github.com/yourusername/klaviyo-webflow.git
cd klaviyo-webflow
npm install
npm run build
```

This will create the distribution files in the `dist` directory.

### Development server

```
npm run dev
```

This will start a development server at http://localhost:8080.

## License

MIT

---

For more examples and details, see the [examples](./examples) directory.

For questions or support, please open an issue on GitHub. 