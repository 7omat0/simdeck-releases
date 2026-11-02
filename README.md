# SimDeck

SimDeck is a macOS menu bar app and command line tool for working with iOS Simulator apps. [한국어](README.ko.md)

This repository only hosts SimDeck releases (DMG files) and its update feed. The source code is not published here.

## Features

- **Deeplinks and pushes**: open URLs and deeplinks in a simulator, and send push notification payloads to an app. Save them per app and reuse them.
- **Location, privacy, status bar**: simulate a fixed location, a route, or a built-in scenario; grant, revoke, or reset privacy permissions; override the status bar (for example, the 9:41 preset).
- **Capture**: save screenshots and screen recordings of a simulator.
- **Design tools**: grid, rulers and guides, a magnifier with color picking, and a design image overlay to compare against the app.
- **Network Monitor**: inspect HTTP requests from simulator apps you start with **Launch with Network Monitor** in the panel, or from apps you run from Xcode when **Connect apps run from Xcode** is on. Copy requests as cURL and export HAR files.
- **Network profiles**: limit the network of selected simulator apps (Airplane Mode, 100% Packet Loss, 3G, Edge, LTE, Wi-Fi, DSL, Very Bad Network) without affecting your Mac or other apps.
- **Command line tool**: the `simdeck` command runs the same actions from Terminal and scripts (`--json` for machine-readable output).
- **Agent commands**: `simdeck ui` lets a coding agent such as Claude Code read the screen of the simulator app chosen in the panel and operate it: tap, type, swipe, scroll, wait, answer system alerts, press device buttons, rotate, switch appearance, and simulate Face ID. It works inside the simulator with an XCTest helper, so it does not move your mouse pointer or take keyboard focus on your Mac.
- **English and Korean**: SimDeck follows your macOS language.

## Requirements

- macOS 15 or later
- Xcode with iOS Simulator runtimes
- Agent commands: a simulator running iOS 18 or later

## Install

1. Download `SimDeck-<version>.dmg` from [Releases](https://github.com/7omat0/simdeck-releases/releases).
2. Open the DMG and drag **SimDeck** to the **Applications** folder. SimDeck must run from `/Applications` to install its network extension, command line tool, and updates.
3. Open SimDeck from Applications. It appears in the menu bar.
4. Optional setup:
   - **Network profiles**: in the panel, open the Network tab and click **Install Extension…**. Allow the extension when macOS asks (System Settings > General > Login Items & Extensions), then allow SimDeck to filter network content.
   - **Design tools**: allow SimDeck in System Settings > Privacy & Security > Accessibility so it can follow the Simulator window.
   - **Command line tool**: in SimDeck Settings, click **Install Command Line Tool…** to create `/usr/local/bin/simdeck` (asks for an administrator password).
   - **Agent skill for Claude Code**: in SimDeck Settings > Agent, click **Install Agent Skill…**. The skill is installed in `~/.claude/skills/simdeck` and tells Claude Code how to use `simdeck ui`. It finds `simdeck` in your `PATH` or inside SimDeck.app, so the command line tool is optional.
   - **Network Monitor for apps run from Xcode**: in SimDeck Settings > Network Monitor, turn on **Connect apps run from Xcode**. SimDeck adds one SimDeck breakpoint to the User breakpoints in Xcode, so apps you run from Xcode on a simulator appear in Network Monitor without code changes. Change this setting while Xcode is closed; if Xcode is open, SimDeck applies the change after you quit Xcode.

## Using the agent commands

1. Boot a simulator and choose the simulator and app in the SimDeck panel. Agent commands only work on that choice.
2. Ask Claude Code to check something in the app, for example "Enter a wrong password on the login screen and check that the error message appears."
3. While the agent works, the panel shows the agent status. The first command on a simulator installs and starts the "SimDeck Agent" helper app on that simulator.

Run `simdeck ui --help` to see all commands.

## Updates

SimDeck checks for updates only when you ask. Click **Check for Updates…** in the panel or in Settings > Updates. Updates are signed and notarized.

## Uninstall

1. In SimDeck Settings, click **Remove Extension…** and approve the request. This removes the network extension and its content filter.
2. Quit SimDeck and move it from Applications to the Trash.
3. If you installed the command line tool, run `sudo rm /usr/local/bin/simdeck` in Terminal.
4. Optional: delete your saved actions and captured network data in `~/Library/Application Support/SimDeck`.
5. Optional: delete the agent skill folder `~/.claude/skills/simdeck`, and remove the "SimDeck Agent" helper app from your simulators (see Known issues).

If you turned on **Connect apps run from Xcode**, turn it off with Xcode closed before step 2. Otherwise you can delete the SimDeck breakpoint from the User breakpoints in Xcode's Breakpoint navigator.

If you move SimDeck to the Trash without step 1, macOS still asks to remove the network extension, but the "SimDeck" content filter may remain in System Settings > Network > Filters. You can delete it there.

## Known issues

- After an update that includes a new network extension, SimDeck may show "Restart your Mac to finish the update." Network profiles work again after a restart.
- Agent commands were built and tested with Xcode 27.1 on iPhone simulators running iOS 27. Other Xcode versions, earlier iOS versions, and iPad simulators have not been tested.
- The "SimDeck Agent" helper app stays installed on each simulator where agent commands ran, and appears on its home screen. To remove it, run `xcrun simctl uninstall <simulator UDID> com.ohisea.simdeck.agentrunner.xctrunner`.
- If another app (not the home screen) is in front of the chosen app, an agent command can wait until its time limit and fail with `helper_timed_out`. SimDeck then restarts the helper, and the next command works normally.
- While breakpoints are deactivated in Xcode (⌘Y), apps run from Xcode do not connect to Network Monitor.
- With **Connect apps run from Xcode**, requests an app makes right after it starts may not appear in Network Monitor.

## Privacy

SimDeck does not collect usage data. Network Monitor data stays on your Mac.
