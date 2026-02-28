# Contributing to Itsytv

Thank you for your interest in contributing! This guide covers everything you need to get started with development, understand the codebase, and submit changes.

## Requirements

- macOS 14.0 or later
- Xcode 15.0 or later
- [XcodeGen](https://github.com/yonaskolb/XcodeGen) for project generation
- Apple TV running tvOS 15 or later on the same local network

## Setup

### 1. Install XcodeGen

```bash
brew install xcodegen
```

### 2. Clone the repository

```bash
git clone https://github.com/nickustinov/itsytv-macos.git
cd itsytv-macos
```

### 3. Generate the Xcode project

```bash
xcodegen generate
```

### 4. Open and run

```bash
open itsytv.xcodeproj
```

Select the **itsytv** scheme and run.

## Architecture

```
itsytv/
├── itsytvApp.swift                # App entry point
├── AppState.swift                 # Shared types (ConnectionStatus, AppleTVDevice)
├── Discovery/
│   └── DeviceDiscovery.swift      # Bonjour discovery of Apple TVs on the local network
├── Protocol/
│   ├── AppleTVManager.swift       # Orchestrator: discovery → pairing → session → commands
│   ├── CompanionConnection.swift  # TCP connection and frame handling
│   ├── CompanionFrame.swift       # Companion Link frame structure (type + length + payload)
│   ├── CompanionCommands.swift    # HID buttons, session start, app launching
│   ├── TextInputSession.swift     # Live text input to Apple TV text fields
│   ├── OPACK.swift                # Apple's OPACK binary serialization format
│   ├── BinaryPlist.swift          # Binary plist encoder with NSKeyedArchiver UIDs
│   └── TLV8.swift                 # TLV8 encoding for HomeKit-style pairing
├── Crypto/
│   ├── CompanionCrypto.swift      # ChaCha20-Poly1305 encryption for Companion protocol
│   ├── CryptoHelpers.swift        # Shared helpers (nonce padding, HKDF-SHA512)
│   ├── PairSetup.swift            # SRP-based pair-setup flow (M1–M6)
│   ├── PairVerify.swift           # Pair-verify flow (M1–M4) with stored credentials
│   └── KeychainStorage.swift      # Secure credential persistence in macOS Keychain
├── AirPlay/
│   ├── AirPlayControlChannel.swift # HTTP/RTSP client with pair-verify and HAP encryption
│   ├── AirPlayPairVerify.swift    # Pair-verify flow (M1–M4) over AirPlay HTTP
│   ├── AirPlayMRPTunnel.swift     # AirPlay tunnel for media remote protocol
│   ├── DataStreamChannel.swift    # MRP protobuf transport over AirPlay 2 with framing
│   ├── HAPChannel.swift           # Base class for HAP-encrypted TCP channels
│   └── HAPSession.swift           # HAP session encryption with block framing
├── MRP/
│   ├── MRPManager.swift           # Now-playing state and media commands
│   ├── NowPlayingState.swift      # Now-playing metadata structure
│   └── Proto/                     # Protobuf definitions and generated Swift code
├── DesignSystem/
│   ├── DesignSystem.swift         # Colours, typography, spacing, sizing tokens
│   └── HighlightingMenuItemView.swift # Custom NSView for interactive menu items
├── AppIntents/
│   └── OpenRemoteIntent.swift     # Shortcuts action to open the remote for a specific Apple TV
├── UI/
│   ├── AppController.swift        # NSStatusItem, menu, floating panel, keyboard monitor
│   ├── MenuBarView.swift          # SwiftUI views: remote, now playing, app grid
│   └── AppIconLoader.swift        # App icons from iTunes Lookup API
└── Utilities/
    ├── AppOrderStorage.swift      # Per-device drag-to-reorder persistence
    ├── UpdateChecker.swift        # GitHub release checker
    └── HotkeyManager.swift        # Global hotkey registration
```

## Building

The project uses XcodeGen to generate the Xcode project from `project.yml`. After making changes to project configuration:

```bash
xcodegen generate
```

## Testing

```bash
xcodebuild test -scheme itsytvTests -destination "platform=macOS"
```

## Releasing

1. Bump `CFBundleShortVersionString` and `CFBundleVersion` in `itsytv/Info.plist`
2. Update `CHANGELOG.md`
3. Build, sign, and package the DMG:

```bash
bash scripts/build-release.sh
```

4. Notarize and staple:

```bash
xcrun notarytool submit dist/itsytv-<VERSION>.dmg \
    --apple-id <APPLE_ID> --team-id <TEAM_ID> \
    --password <APP_SPECIFIC_PASSWORD> --wait
xcrun stapler staple dist/itsytv-<VERSION>.dmg
```

5. Create the GitHub release:

```bash
gh release create v<VERSION> dist/itsytv-<VERSION>.dmg \
    --title "v<VERSION>" --notes "Release notes here"
```

6. Update the Homebrew cask:

```bash
brew bump-cask-pr itsytv --version <VERSION>
```
