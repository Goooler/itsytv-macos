# Itsytv

[![Tests](https://github.com/nickustinov/itsytv-macos/actions/workflows/tests.yml/badge.svg)](https://github.com/nickustinov/itsytv-macos/actions/workflows/tests.yml)
[![Release](https://img.shields.io/github/v/release/nickustinov/itsytv-macos)](https://github.com/nickustinov/itsytv-macos/releases/latest)
[![Downloads](https://img.shields.io/github/downloads/nickustinov/itsytv-macos/total)](https://github.com/nickustinov/itsytv-macos/releases)
[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Swift 5.10](https://img.shields.io/badge/swift-5.10-orange.svg)](https://swift.org)
[![macOS 14+](https://img.shields.io/badge/macOS-14%2B-brightgreen.svg)](https://www.apple.com/macos/sonoma/)
[![Homebrew](https://img.shields.io/badge/homebrew-cask-yellow.svg)](https://formulae.brew.sh/cask/itsytv)

A native macOS menu bar app for controlling your Apple TV.

[![Download on the Mac App Store](https://developer.apple.com/app-store/marketing/guidelines/images/badge-download-on-the-mac-app-store.svg)](https://apps.apple.com/app/itsytv/id6759216148)

❤️ If you enjoy Itsytv, grab the App Store version to support development and get automatic updates.

![itsytv hero](https://itsytv.app/itsytv-hero.png)

## Features

- **Menu bar remote** — Control your Apple TV from a compact floating panel
- **D-pad and buttons** — Circular d-pad with directional navigation, select, home, menu/back, play/pause
- **Keyboard navigation** — Arrow keys, Return, Backspace, Escape, Space mapped to remote buttons
- **Text input** — Type directly into Apple TV text fields with a live keyboard
- **Now playing** — Artwork, title, artist, progress bar, and playback controls
- **App launcher** — Grid of installed apps with icons fetched from the App Store; drag to reorder
- **Multiple devices** — Pair and switch between multiple Apple TVs
- **Global hotkeys** — Assign keyboard shortcuts to instantly open the remote for specific Apple TVs
- **Per-device panel position** — Remembers where you placed the remote for each Apple TV
- **Launch at login** — Optional auto-start from the menu bar
- **Unpair** — Remove pairing credentials from the panel menu

## Perfect companion to Itsyhome

Itsytv pairs naturally with [Itsyhome](https://itsyhome.app) — a free macOS menu bar app for controlling your HomeKit devices. Manage lights, cameras, thermostats, locks, scenes, and 18+ accessory types without ever opening the Home app.

![Itsyhome](https://itsytv.app/itsyhome.png)

## Install

```bash
brew install --cask itsytv
```

Or download the latest DMG from [GitHub releases](https://github.com/nickustinov/itsytv-macos/releases).

## Troubleshooting

### Apple TV doesn't show a PIN code when pairing

If you send a pairing request but no PIN appears on your TV screen, your Apple TV is likely restricting which devices can connect to it. To fix this:

1. Open **Settings → AirPlay and Apple Home** on your Apple TV
2. Set **Allow access** to **Anyone on the same network**
3. Go to **Settings → General → Restrictions**
4. Set both **AirPlay Settings** and **Remote App Pairing** to **Allow**

This setting needs to stay on this value for itsytv to maintain a connection to your Apple TV.

### Remote disappears after a few seconds

If the remote panel closes on its own shortly after connecting, your Apple TV's AirPlay access setting is likely set to **Only people sharing this home**. Open **Settings** on your Apple TV, go to **AirPlay and Apple Home**, and change **Allow access** to **Anyone on the same network**.

### Nothing happens when I launch the app

Itsytv is a menu bar app — it lives in the top-right area of your screen as a small TV icon, not in the Dock. On MacBooks with a notch, macOS hides menu bar icons that don't fit behind the notch — silently, with no warning. If your menu bar is crowded, the itsytv icon may be there but invisible.

To fix this, hold **⌘ Cmd** and drag any icons you don't need off the menu bar. Once itsytv appears, ⌘-drag it to the right so it stays visible.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for setup instructions, architecture overview, build steps, testing, and the release process.

## License

MIT License © 2026 Nick Ustinov — see [LICENSE](LICENSE) for details.

## Author

**Nick Ustinov**
- GitHub: [@nickustinov](https://github.com/nickustinov)

## Acknowledgements

Protocol implementation informed by [pyatv](https://github.com/postlund/pyatv), the comprehensive Python library for Apple TV control.
