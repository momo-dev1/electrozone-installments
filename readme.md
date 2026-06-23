# Installment Plans - Standalone Module

This folder contains the complete Installment Plans functionality extracted from the main ElectroZone application.

## Files Structure

```
Installment Plans/
├── bank/                    # Bank logo images (webp format)
├── bnpl/                    # BNPL company logo images (webp format)
├── installment-plans.html   # Main HTML file (all-in-one version)
├── installment-plans.css    # Separate CSS file
├── installment-plans.js     # Separate JavaScript file
└── README.md               # This file
```

## Features

- **BNPL & Banks Support**: Switch between Buy Now Pay Later companies and traditional banks
- **Price Calculator**: Enter product price and downpayment to calculate installment plans
- **Dynamic Filtering**: Filter by company/bank and duration
- **Brand Logos**: Visual display of all supported BNPL companies and banks
- **Dark Mode**: Built-in theme switcher with localStorage persistence
- **Responsive Design**: Mobile-friendly interface
- **Google Sheets Integration**: Loads data from Google Sheets in CSV format

## Usage

### Option 1: All-in-One HTML
Simply open `installment-plans.html` in any modern web browser. All CSS and JavaScript are embedded.

### Option 2: Separate Files (For Development)
If you want to modify CSS or JS separately, you can link the external files:

1. Update the HTML file to include:
```html
<link rel="stylesheet" href="installment-plans.css">
<script src="installment-plans.js"></script>
```

2. Remove the inline `<style>` and `<script>` tags from the HTML

## Configuration

### Google Sheet ID
The installment data is loaded from a Google Sheet. To use your own sheet:

1. Open `installment-plans.js` (or the `<script>` section in the HTML)
2. Find the line:
```javascript
const INSTALLMENT_SHEET_ID = "1diLfTHgQAiruCK100OrQRFg7JvJZU4BS";
```
3. Replace with your Google Sheet ID

### Required Sheet Columns
Your Google Sheet must have these columns:
- `Platform`: The platform name (e.g., "Online", "In-Store")
- `Bank Account`: The bank or BNPL company name
- `Duration`: Duration in months (e.g., "12", "24")
- `Interest Rate`: Interest rate (e.g., "3%", "0.03", or "3")
- `Admin Fees`: Admin fees (e.g., "2%", "0.02", or "2")
- `Type`: Either "bnpl" or "bank"

### Brand Logos
Brand logos are stored in the same directory:
- BNPL logos: `bnpl/[company-name].webp`
- Bank logos: `bank/[bank-name].webp`

All logo images are included in the `bank/` and `bnpl/` folders. If you move or reorganize these folders, update the paths in the `BRAND_CONFIG` object in the JavaScript.

## Dependencies

- **Google Fonts**: Manrope font family (loaded via CDN)
- **No external JavaScript libraries**: Pure vanilla JavaScript

## Browser Support

- Chrome/Edge (latest)
- Firefox (latest)
- Safari (latest)
- Mobile browsers (iOS Safari, Chrome Mobile)

## Development Notes

### Theme System
The theme is stored in `localStorage` with the key `"theme"`. Values: `"light"` or `"dark"`.

### Data Flow
1. On page load, `loadInstallmentData()` fetches CSV from Google Sheets
2. Data is parsed and stored in `installmentPlansRawData`
3. Users can filter by type (BNPL/Banks), company, and duration
4. Calculations are performed in `calculateInstallments()` based on selected filters

### Key Functions
- `loadInstallmentData()`: Fetches and parses data from Google Sheets
- `selectInstallmentType(type, el)`: Switches between BNPL and Banks
- `selectInstallmentCompany(name)`: Selects a specific company/bank
- `calculateInstallments()`: Calculates and displays installment plans
- `toggleTheme()`: Switches between light and dark mode

## Future Improvements

Potential enhancements you can make:
1. Add export functionality (PDF, Excel)
2. Add print-friendly styling
3. Add comparison mode to compare multiple plans
4. Add email/share functionality
5. Add currency converter
6. Add search/filter by platform name
7. Cache Google Sheets data with service worker

## License

Part of the ElectroZone Internal System
