# StreaMar IPTV

A cross-platform desktop IPTV player application built with Tauri, React, and TypeScript.

## Features

- **Clean, Modern UI**: Glassy minimal design inspired by GitHub, Discord, and Vercel
- **Xtream Codes API Support**: Full integration with Xtream Codes IPTV providers
- **Secure Storage**: Credentials stored in OS keychain, never in plain text
- **Multiple Content Types**: Live TV, Movies, and Series
- **Continue Watching**: Automatically tracks playback position
- **Watchlist & History**: Save favorites and track viewing history
- **Search**: Fast, debounced search across all content
- **Settings**: Theme customization, privacy controls, and account management

## Important Compliance Notice

This application is designed for **legitimate, authorized IPTV subscriptions only**. You must have legal rights to access the content you stream. The app does not host, restream, rebroadcast, scrape, or provide any built-in catalog.

## Prerequisites

- Node.js 18+ and npm
- Rust (for Tauri)
- System dependencies for Tauri (see [Tauri prerequisites](https://tauri.app/v1/guides/getting-started/prerequisites))

## Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd "StreaMar IPTV"
```

2. Install dependencies:
```bash
npm install
```

3. Run in development mode:
```bash
npm run tauri:dev
```

## Building

To build the application for production:

```bash
npm run tauri:build
```

The built application will be in `src-tauri/target/release/`.

## Usage

1. **First Launch**: You'll be prompted to accept the compliance disclaimer
2. **Add Account**: Enter your IPTV provider details (Server URL, Username, Password)
3. **Browse**: Navigate through Live TV, Movies, and Series
4. **Play**: Click on any item to start playback
5. **Manage**: Use the Library section to view your watchlist and history

## Keyboard Shortcuts (Player)

- `Space`: Play/Pause
- `←` / `→`: Seek backward/forward 10 seconds
- `↑` / `↓`: Increase/decrease volume
- `F`: Toggle fullscreen
- `M`: Mute/unmute
- `Esc`: Exit fullscreen or go back

## Project Structure

```
src/
  app/              # Routing and layout
  features/         # Feature modules (auth, catalog, player, etc.)
  services/         # API clients and business logic
  storage/          # Database and secure storage
  ui/               # Reusable UI components
  stores/           # Zustand state management
```

## Troubleshooting

### Connection Issues

- Verify your server URL is correct (should include protocol: `https://example.com`)
- Check that your credentials are valid
- Ensure your IPTV provider supports Xtream Codes API

### Playback Issues

- Some streams may require specific codecs or DRM support
- Check your internet connection
- Try a different stream if available

### Build Issues

- Ensure Rust is properly installed: `rustc --version`
- Clear build cache: `cd src-tauri && cargo clean`
- Reinstall dependencies: `rm -rf node_modules && npm install`

## Development

The project uses:
- **Tauri v2** for desktop app framework
- **React 18** with TypeScript
- **Vite** for build tooling
- **Tailwind CSS** for styling
- **Zustand** for state management
- **TanStack Query** for data fetching
- **SQLite** (via Tauri plugin) for local storage

## License

This project is for educational and legitimate use only. Users are responsible for ensuring they have proper authorization to access any content streamed through this application.
