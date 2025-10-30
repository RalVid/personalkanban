# PWA (Progressive Web App) Setup

This application is now installable as a Progressive Web App!

## What's Been Added

1. **manifest.json** - Web app manifest that defines how the app appears when installed
2. **sw.js** - Service worker for offline functionality and caching
3. **Updated index.html** - Added manifest link, theme colors, and service worker registration
4. **Icon placeholders** - SVG icons (icon-192.svg and icon-512.svg)

## How to Install

### Desktop (Chrome/Edge)
1. Visit the website
2. Look for the install icon in the address bar (⊕ or computer icon)
3. Click "Install" when prompted

### Mobile (Chrome/Safari)
1. Visit the website
2. Tap the browser menu (⋮ or share icon)
3. Select "Add to Home Screen" or "Install App"

## Icon Replacement

The current icons are simple SVG placeholders with a "K" letter. To create proper icons:

1. **Convert SVG to PNG:**
   - Use online tools like [CloudConvert](https://cloudconvert.com/svg-to-png)
   - Or use design software (Figma, Inkscape, GIMP)

2. **Create custom icons:**
   - Design 192x192px and 512x512px PNG images
   - Use your preferred design tool
   - Recommended: Use a kanban board visual (columns with cards)
   - Colors: Green (#22c55e) on dark background (#0f172a)

3. **Replace files:**
   - Replace `icon-192.svg` with `icon-192.png`
   - Replace `icon-512.svg` with `icon-512.png`
   - Update `manifest.json` if you change the file names

## Testing

1. **Local testing:**
   - Run a local web server: `python -m http.server 8000` or `npx serve`
   - Navigate to `http://localhost:8000`
   - Note: PWA installation requires HTTPS (except localhost)

2. **GitHub Pages:**
   - Push changes to GitHub
   - Enable GitHub Pages in repository settings
   - The app will be installable at your GitHub Pages URL

## Features

- ✅ Works offline after first visit
- ✅ Installable on desktop and mobile
- ✅ Standalone window (no browser UI)
- ✅ Fast loading with caching
- ✅ Firebase cloud sync still works when online

## Customization

Edit `manifest.json` to customize:
- `name` - Full app name
- `short_name` - Name shown on home screen
- `description` - App description
- `theme_color` - Browser theme color
- `background_color` - Splash screen background

## Browser Support

- ✅ Chrome/Edge (Desktop & Mobile)
- ✅ Safari (iOS 11.3+)
- ✅ Firefox (Desktop & Mobile)
- ✅ Samsung Internet
- ⚠️ Some features may vary by browser
