# Personal Kanban Board

Keep track of your tasks in your private Kanban board with optional Google account sync.

## Features

✨ **Simple & Clean** - Minimalist dark theme interface
📝 **Task Headlines & Descriptions** - Organize with titles and detailed notes
🎯 **Three Columns** - To Do, Doing, Done
🖱️ **Drag & Drop** - Easy task management
✏️ **Editable Board Name** - Customize your board title
💾 **Local Storage** - Works offline, saves automatically
☁️ **Google Sync** (Optional) - Sync across devices with your Google account
🔒 **Private & Secure** - Your data stays in your browser or your Google account

## Quick Start

1. Clone or download this repository
2. Open `index.html` in your browser
3. Start adding tasks!

## Google Sync Setup

To enable syncing across devices with your Google account:

1. Follow the [Firebase Setup Guide](FIREBASE_SETUP.md)
2. Update the Firebase configuration in `index.html`
3. Deploy to a web server (GitHub Pages, Netlify, etc.)

**Note**: Google sync is optional. The app works perfectly fine with local storage only.

## Usage

- **Add Task**: Type a headline and press "Lägg till"
- **Edit Task**: Double-click any task card
- **Move Task**: Drag and drop between columns
- **Delete Task**: Click "Ta bort" on the task
- **Edit Board Name**: Click the board title at the top
- **Export/Import**: Use buttons to backup/restore your board
- **Sign In**: Click "🔐 Logga in" to enable Google sync

## Local Development

Simply open `index.html` in your browser. No build process needed!

## Deployment

### GitHub Pages (Free)

1. Push to GitHub
2. Go to repository Settings > Pages
3. Select branch and save
4. Your app will be live at `https://yourusername.github.io/personalkanban/`

### Other Options

- Netlify (drag & drop)
- Vercel
- Any static hosting service

## Technical Details

- Pure HTML/CSS/JavaScript (no frameworks)
- Firebase for authentication and sync (optional)
- Responsive design
- localStorage for offline support

## Browser Support

Modern browsers (Chrome, Firefox, Safari, Edge)

## License

Free to use and modify.

