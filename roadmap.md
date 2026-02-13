You are Cursor AI acting as a senior full-stack desktop engineer + product designer.

Build a cross-platform desktop app named **StreaMar IPTV** (Windows/macOS/Linux). The app is a **client/player only**: it must NOT host, restream, rebroadcast, scrape, or provide any built-in catalog. Users bring their own **Xtream Codes / IPTV provider** details (base URL + username + password). The app only consumes provider endpoints and plays streams locally.

IMPORTANT COMPLIANCE
- Build for legitimate, authorized IPTV subscriptions only.
- No “free IPTV”, no bundled playlists, no default servers, no discovery of third-party sources.
- Include an in-app disclaimer + “I confirm I have rights to access this content” checkbox on first run.
- Respect DRM: if a stream is DRM-protected and cannot play, show a helpful error.

PRODUCT GOAL
A clean, modern, minimal, glassy UI (smooth + light). No emojis. Use simple symbols (•, ›, +, ⌘, etc).
Visual inspiration: GitHub + Discord + Vercel aesthetics (neutral, crisp typography, subtle borders).
UX inspiration: Netflix (browse, continue watching, details page, search, watchlist).

TECH STACK (choose one and commit; default to this)
- Tauri v2 + React + TypeScript + Vite
- State: Zustand (or Redux Toolkit if needed)
- Data fetching: TanStack Query
- Styling: Tailwind + CSS backdrop blur for glass effect
- Player engine: mpv (libmpv) embedded, because IPTV streams can be HLS, MPEG-TS, etc. mpv supports many formats and streaming sources. Provide a thin wrapper for playback controls. :contentReference[oaicite:0]{index=0}
- Secure storage: OS keychain (keyring). Never store credentials in plain text.
- Local DB: SQLite (via Tauri plugin) or IndexedDB if simpler; store metadata, favorites, history, continue-watching positions.

CORE IPTV / XTREAM INTEGRATION (must implement)
1) Login / validation
- Input fields: “Server URL”, “Username”, “Password”
- Validate by calling Xtream API and showing account/server info if available.

2) Catalog fetching using Xtream Codes API patterns
- Support fetching:
  - Live categories: `action=get_live_categories`
  - Live streams by category: `action=get_live_streams&category_id=...`
  - VOD categories: `action=get_vod_categories`
  - VOD streams: `action=get_vod_streams` (+ optional category_id)
  - Series categories: `action=get_series_categories`
  - Series list: `action=get_series` (+ optional category_id)
  - VOD info: `action=get_vod_info&vod_id=...`
Use the common `player_api.php?username=...&password=...&action=...` style. :contentReference[oaicite:1]{index=1}

3) Playlist option (fallback)
- Allow importing via the common Xtream “get.php” M3U endpoint (user provides nothing except their same credentials):
  - `get.php?username=...&password=...&type=m3u_plus&output=ts`
Parse M3U and map items to internal models. :contentReference[oaicite:2]{index=2}

4) Playback URL generation
- Implement a provider-agnostic “playback URL builder” that can generate playable URLs for:
  - Live item
  - VOD item
  - Series episode
Do NOT hardcode any specific piracy provider domains. Build strictly from the user’s base URL and the IDs returned by the API.

DATA MODELS (organized, typed, clean)
Create TypeScript models (interfaces) for:
- ProviderAccount { id, name, baseUrl, username, encryptedPasswordRef, createdAt, lastUsedAt }
- Category { id, type: 'live'|'vod'|'series', name, order }
- Stream { id, name, type, categoryId, iconUrl, epgChannelId?, hasCatchup?, … }
- VodItem { id, name, year?, rating?, posterUrl, categoryId, duration?, … }
- Series { id, name, posterUrl, categoryId, seasons: SeasonSummary[] }
- Episode { id, seriesId, seasonNumber, episodeNumber, name, duration?, streamUrl? }
- PlaybackState { itemKey, positionMs, durationMs, updatedAt }
- UI: SearchQuery, Filters, SortMode, ThemeMode

APP INFORMATION ARCHITECTURE (Netflix-like)
Left sidebar (icons + labels):
- Home
- Live TV
- Movies
- Series
- Search
- Library (Watchlist, History)
Top bar:
- Search field (global)
- Account switcher
- Settings

HOME
- Continue Watching row
- Favorites row
- Recently Added (from provider data if possible)
- “Live Now” quick row

LIVE
- Category list on the left, channel grid/list on right
- “Now Playing” mini bar at bottom
- Optional EPG placeholder (only if provider exposes it; keep it modular)

MOVIES / SERIES
- Grid cards, fast scrolling, skeleton loading
- Detail page: poster, description, metadata, play button, add to watchlist

PLAYER VIEW
- Fullscreen player
- Minimal controls: play/pause, seek (for VOD), volume, captions toggle (if available), quality/track selection if mpv exposes it
- Keyboard shortcuts (space, arrows, f, esc, m)
- Remember playback position (continue watching)

SETTINGS
- Appearance: Light/Dark/System
- Streaming: buffer size, user-agent override (optional), hardware decode toggle
- Privacy: “Clear history”, “Remove account”
- About: version, disclaimer

PERFORMANCE + QUALITY
- Smooth scrolling, virtualization for large lists
- Caching with TTL for categories/items
- Debounced search
- Robust error handling with friendly messages (401/403, timeouts, invalid baseUrl)
- Logging panel for debugging (opt-in)

PROJECT STRUCTURE (suggested)
src/
  app/ (routing, layout)
  features/
    auth/
    catalog/
    player/
    search/
    library/
    settings/
  services/
    xtream/
      client.ts (HTTP)
      endpoints.ts
      m3u.ts (parser)
      urlBuilder.ts
      types.ts
  storage/
    db.ts
    secureStore.ts
  ui/
    components/
    theme/
  utils/

DELIVERABLES
- A working Tauri desktop app repo with:
  - polished UI (glassy minimal)
  - account add/switch
  - fetch catalog via Xtream API (player_api.php)
  - fallback import via get.php M3U
  - playback with embedded mpv
  - watchlist + continue watching
  - settings + secure storage
- Include a short README with setup/run steps and troubleshooting.

IMPLEMENTATION PLAN (Cursor, follow strictly)
1) Scaffold Tauri + React + TS + Tailwind project
2) Build UI shell (sidebar/topbar/routes)
3) Implement secure account storage
4) Implement Xtream client + models + caching
5) Build Live/Movies/Series pages with virtualization
6) Implement mpv playback module + controls + shortcuts
7) Add history/continue watching + watchlist
8) Add settings + theming + polish animations (subtle, fast)
9) QA with fake/mock provider responses (include mock JSON fixtures); never ship real credentials

NOTES
- Keep code clean, strongly typed, and modular.
- Use symbols instead of emojis.
- Make everything feel “GitHub/Discord/Vercel” clean, and “Netflix” in browsing flow.

Start by generating the full repo structure and the key files, then iterate feature by feature in commits/steps.