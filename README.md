# SimDeck

SimDeck is a macOS menu bar app and command line tool for working with iOS Simulator apps. [한국어](README.ko.md)

This repository only hosts SimDeck releases (DMG files) and its update feed. The source code is not published here.

## Features

- **Deeplinks and pushes**: open URLs and deeplinks in a simulator, and send push notification payloads to an app. Save them per app and reuse them.
- **Location, privacy, status bar**: simulate a fixed location, a route, or a built-in scenario; grant, revoke, or reset privacy permissions; override the status bar (for example, the 9:41 preset).
- **Capture**: save screenshots and screen recordings of a simulator.
- **Design tools**: grid, rulers and guides, a magnifier with color picking, and a design image overlay to compare against the app.
- **Network Monitor**: inspect HTTP requests from simulator apps you start with **Launch with Network Monitor** in the panel, copy them as cURL, and export HAR files.
- **Network profiles**: limit the network of selected simulator apps (Airplane Mode, 100% Packet Loss, 3G, Edge, LTE, Wi-Fi, DSL, Very Bad Network) without affecting your Mac or other apps.
- **Command line tool**: the `simdeck` command runs the same actions from Terminal and scripts (`--json` for machine-readable output).
- **English and Korean**: SimDeck follows your macOS language.

## Requirements

- macOS 15 or later
- Xcode with iOS Simulator runtimes

## Install

1. Download `SimDeck-<version>.dmg` from [Releases](https://github.com/7omat0/simdeck-releases/releases).
2. Open the DMG and drag **SimDeck** to the **Applications** folder. SimDeck must run from `/Applications` to install its network extension, command line tool, and updates.
3. Open SimDeck from Applications. It appears in the menu bar.
4. Optional setup:
   - **Network profiles**: in the panel, open the Network tab and click **Install Extension…**. Allow the extension when macOS asks (System Settings > General > Login Items & Extensions), then allow SimDeck to filter network content.
   - **Design tools**: allow SimDeck in System Settings > Privacy & Security > Accessibility so it can follow the Simulator window.
   - **Command line tool**: in SimDeck Settings, click **Install Command Line Tool…** to create `/usr/local/bin/simdeck` (asks for an administrator password).

## Updates

SimDeck checks for updates only when you ask. Click **Check for Updates…** in the panel or in Settings > Updates. Updates are signed and notarized.

## Uninstall

1. In SimDeck Settings, click **Remove Extension…** and approve the request. This removes the network extension and its content filter.
2. Quit SimDeck and move it from Applications to the Trash.
3. If you installed the command line tool, run `sudo rm /usr/local/bin/simdeck` in Terminal.
4. Optional: delete your saved actions and captured network data in `~/Library/Application Support/SimDeck`.

If you move SimDeck to the Trash without step 1, macOS still asks to remove the network extension, but the "SimDeck" content filter may remain in System Settings > Network > Filters. You can delete it there.

## Known issues

- After an update that includes a new network extension, SimDeck may show "Restart your Mac to finish the update." Network profiles work again after a restart.

## Privacy

SimDeck does not collect usage data. Network Monitor data stays on your Mac.
