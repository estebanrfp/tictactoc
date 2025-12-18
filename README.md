# Tic Tac Toe | Minimalist Premium & Real-time P2P

![Preview](assets/preview.webp)

A stunningly minimalist, high-performance Tic Tac Toe game. Enhanced with **real-time multiplayer capabilities** powered by **GenosDB**, allowing decentralized P2P matches without a central server.

## ✨ Features

### 🎮 Multiplayer
- **Real-time P2P Sync**: Decentralized synchronization using GenosDB WebRTC channels.
- **Room System**: Create or join specific game rooms using a unique room name.
- **Instant Updates**: Moves appear instantly on all connected clients.
- **Share Link**: One-click copy of room URL to invite players.

### 👥 Player Roles
- **Player X** (Pink badge): First player to create/join a room.
- **Player O** (Cyan badge): Second player to join.
- **Spectator Mode** (Yellow badge): Third+ connections watch in real-time.
  - Spectators see all moves with "X's Turn" / "O's Turn" indicators.
  - Reset button is disabled for spectators.
  - Live spectator count displayed to all players.

### 🎨 Design
- **Premium Glassmorphic UI**: Vibrant neon accents and smooth transitions.
- **Color-coded Badges**: Visual indicators for player roles.
- **Responsive Layout**: Optimized for mobile, tablet, and desktop.
- **Modern Typography**: Inter & Outfit fonts.

### ⚡ Technical
- **Ultra-Compact**: Single standalone HTML file (~26KB).
- **Zero Dependencies**: Pure vanilla JS (ES2024 style).
- **Top-level Await**: GenosDB initializes at page load for instant P2P.

## 🚀 How to Play

### 1. Start a Game
```bash
bun x serve ./
# or: npx serve ./
```
Open `http://localhost:3000` in your browser.

### 2. Create a Room
1. Enter a room name (e.g., `my-game-2024`)
2. Click "Join Room"
3. You'll be assigned as **Player X**

### 3. Invite Others
1. Click **"Copy Link"** button
2. Share the URL with friends
3. Second player becomes **Player O**
4. Additional players become **Spectators**

### 4. Play!
- X always goes first
- Board is disabled when waiting for opponent
- Winners are highlighted with golden cells
- Click "Reset Match" or "Play Again" to restart

## 🔧 Architecture

```
┌─────────────────────────────────────────────────────────┐
│                    GenosDB (P2P Layer)                  │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐     │
│  │  Player X   │◄─►│  Player O   │◄─►│ Spectators  │     │
│  │   (Room)    │   │   (Room)    │   │   (Room)    │     │
│  └─────────────┘   └─────────────┘   └─────────────┘     │
│         ▲                 ▲                 ▲            │
│         │    WebRTC Data Channels          │            │
│         └─────────────────┴─────────────────┘            │
└─────────────────────────────────────────────────────────┘
```

- **Database**: [GenosDB](https://github.com/estebanrfp/gdb) for real-time P2P synchronization.
- **Channels**: `db.room.channel("game-state")` for instant move broadcasting.
- **Presence**: `room.on("peer:join/leave")` for player/spectator tracking.
- **Persistence**: Game state persisted via `db.put()` for late joiners.

## 📋 Browser Requirements
- Modern browser with WebRTC support
- Must be served via HTTP/HTTPS (not `file://` protocol)

## 📄 License
MIT License - see [LICENSE.md](LICENSE.md)

## Author

Esteban Fuster Pozzi (@estebanrfp) — Full Stack JavaScript Developer
