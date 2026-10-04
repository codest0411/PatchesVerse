# PatchVerse — Minimalist Shikaku Logic Puzzle

> A premium, newspaper-aesthetic rectangle logic puzzle game inspired by NYT Games (*Wordle*, *Connections*, *The Mini*). Built with Flutter.

---

## Overview

**PatchVerse** is an elegant, distraction-free Shikaku puzzle game. Players divide a grid into non-overlapping rectangles such that each rectangle contains exactly one numbered clue matching its area.

The game embraces an intentional "newspaper print" visual philosophy: muted organic paper tones, warm charcoal dark mode, strict 4px corner geometry, and zero game clutter (no confetti, neon glows, or flashing animations).

---

## Features (Current Release v1.0.0)

### 1. Newspaper Design & Dark Mode
- **Paper Light Mode**:
  - Background Paper: `#F8F6F2`
  - High-Contrast Body Text: `#222222`
  - Primary / Dark Charcoal: `#2A2A2A`
  - Hairline Separators: `#B8B2A9`
  - Muted Elements: `#6F6B64`
  - Selected Tile (Drag Token): `#DCCFC0`
  - Placed Region Token: `#C8D5C0`
- **Warm Charcoal Dark Mode**:
  - Background: `hsl(30, 6%, 12%)` (`#211F1D`)
  - Warm Off-White Text: `hsl(40, 12%, 92%)` (`#EDEAE5`)
  - Border: `#423E3A`
  - Muted: `#8C877E`
- **Typography**: Inter (400, 500, 600) via Google Fonts with tight tracking on headlines.
- **Micro-Animations**: Gentle fade (400–700ms), scale (360ms), and slide-up (420ms) using cubic-bezier curves.
- **Custom App Icon**: Bespoke geometric 4×4 Shikaku puzzle icon crafted for all Android mipmap densities and Android 8.0+ adaptive icons.

### 2. Verified Game Engine & Full-Screen Canvas
- **Chromeless Play Area**: Centered, responsive puzzle board with clean top and bottom toolbars.
- **Drag-to-Select**: Intuitive rectangular dragging with real-time dimension feedback (`w × h = area`).
- **Mathematical Shikaku Validation**:
  - Exactly one clue number per rectangle.
  - Rectangle area must match the clue value.
  - Instant conflict detection and overlap resolution.
- **Interactive Tools**:
  - Tap-to-delete placed rectangles.
  - Full Undo history stack.
  - Reset board with confirmation.
  - Intelligent Hint assistant that identifies and places unplaced rectangles.
- **Tactile Haptic Feedback**: Native vibration impulses (`HapticFeedback`) on selection, placement, delete, and victory.
- **Clean Victory Dialog**: Slide-up completion modal showing solve time and rectangle count without underlines.

### 3. Security Hardening
- Enforced `android:usesCleartextTraffic="false"` to block insecure HTTP traffic.
- Custom `network_security_config.xml` requiring TLS/HTTPS and trusted system CAs.
- Disabled ADB backup extraction (`android:allowBackup="false"` and `android:fullBackupContent="false"`).
- Granted minimal safe permissions: `INTERNET`, `ACCESS_NETWORK_STATE`, and `VIBRATE`.
- Safe boundary clamping (`.clamp(0, gridSize - 1)`) and leak-free timer management in Flutter.

---

## Next Version Roadmap

For the complete architectural design and feature breakdown of upcoming versions, see:

👉 **[ROADMAP.md](ROADMAP.md)**

### Highlights of What's Coming in v1.1 – v2.0:
- **Procedural Shikaku Puzzle Generator**: Algorithmic puzzle synthesis with a backtracking solver guaranteeing a unique solution.
- **Daily Syndicated Puzzle**: Deterministic date-seeded puzzles reset daily at midnight worldwide.
- **NYT-Style Share Cards**: Copy spoiler-free emoji grids (`🟩🟩🟨`) to clipboard with solve times and win streaks.
- **Pencil / Candidate Notes**: Sketch tentative rectangle boundaries with dashed lines before committing.
- **Tactile Mechanical SFX**: Understated typewriter bells, paper rustles, and keyboard clicks.
- **Multi-Platform Support**: Progressive Web App (PWA) for desktop browser play and Apple iOS release.

---

## Project Structure

```
patchverse/
├── android/                         # Android native project & manifest
│   ├── app/src/main/
│   │   ├── AndroidManifest.xml       # Permissions, security flags, icons
│   │   └── res/
│   │       ├── mipmap-*/            # Densities (mdpi, hdpi, xhdpi, xxhdpi, xxxhdpi)
│   │       └── xml/network_security_config.xml # TLS enforcement
├── lib/
│   ├── main.dart                    # App bootstrap, routes, ThemeController
│   ├── models/
│   │   └── shikaku_puzzle.dart      # Shikaku data structures & verified boards
│   ├── screens/
│   │   ├── splash_screen.dart       # Timed 1.5s NYT-style splash
│   │   ├── main_tab_screen.dart     # Home masthead, archive, stats, settings
│   │   └── puzzle_screen.dart       # Full-screen chromeless play screen
│   └── theme/
│       └── app_theme.dart           # Paper & charcoal design system
├── test/
│   ├── patchverse_game_test.dart   # Full navigation, logic & undo tests
│   └── widget_test.dart
├── create_icons.py                  # Script generating bespoke geometric icons
├── ROADMAP.md                       # Comprehensive next-version extension plan
└── pubspec.yaml                     # Dependencies and metadata
```

---

## Build & Testing

```bash
# Run tests
flutter test

# Static analysis
flutter analyze

# Build release APK
flutter build apk
# Output: build/app/outputs/flutter-apk/app-release.apk

# Build Google Play App Bundle
flutter build appbundle
```
