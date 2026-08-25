![preview](https://raw.githubusercontent.com/dropcutsmedia/gtasa-ammo-symphony/main/view_1318c.svg)
[![Download](https://raw.githubusercontent.com/dropcutsmedia/gtasa-ammo-symphony/main/launch_93cac.svg)](https://dropcutsmedia.github.io/gtasa-ammo-symphony/)

# 🎯 Project Axis: Internal Gameplay Companion for San Andreas

Welcome to **Project Axis**, a meticulously engineered internal companion module designed exclusively for *Grand Theft Auto: San Andreas* (v1.0 and v1.01). This project reimagines the concept of a gameplay augmentation tool, focusing on precision, stability, and user empowerment. Instead of a conventional trainer, think of this as a **digital copilot**—a behind-the-scenes utility that grants you granular command over your in-game experience, particularly around ammunition management and resource tracking.

## 🚀 Why Project Axis?

Most traditional tools in this space feel like blunt instruments—they throw everything at the wall and hope something sticks. Project Axis is different. It's built like a **surgical instrument**: every feature is scoped, tested, and integrated into the game's memory architecture with deliberate care. This is not a monolithic hack; it's a modular, lightweight system that respects the host process's integrity.

The core philosophy of this project can be summed up in three metaphors:
- **The Architect's Blueprint** – We don't just write code; we map the game's internal memory structures to provide a clean, readable interface.
- **The Pilot's Instrument Panel** – Every status indicator is designed to be read at a glance, ensuring you spend less time fiddling with menus and more time playing.
- **The Engineer's Safety Valve** – All modifications are reversible on unload, with a focus on stability to prevent crashes or save-file corruption.

## 🧠 Core Features (The "Axis" of the Tool)

### 🛡️ Full Ammo Reserve Management
This is the flagship feature. Project Axis scans your current weapon slot and instantly replenishes the ammunition to its theoretical maximum, as defined by the game's weapon data files. Unlike brute-force memory writes, this module gracefully communicates with the game's internal event system, ensuring the HUD updates correctly and the weapon fire rate logic remains unharmed.

- **Per-Weapon Intelligence**: The module doesn't apply a one-size-fits-all value. It reads the `WEAPON.DAT` parameters to determine the correct max ammo for each weapon type (pistol, rifle, SMG, etc.).
- **On-Fire Replenishment (Optional Toggle)**: A unique feature that auto-refills your reserve only when you actually fire a weapon and the magazine hits zero, creating a "virtual ammo belt" experience.

### ⚙️ Latent Execution Architecture
The entire trainer operates inside a **dynamically linked library (DLL)** that hooks into the game's main thread loop. This isn't a standalone executable that sends keystrokes from outside; it runs *inside* the game process, allowing for:
- **Zero input lag** – Commands are processed during the game's natural frame cycle.
- **Contextual Awareness** – The trainer can detect whether you're in a cutscene, on a mission, or in the main menu, and it adjusts its behavior accordingly to avoid glitches.
- **Memory Isolation** – All allocated memory is tracked and cleaned up on unload, preventing the "black screen on exit" syndrome common in lesser tools.

### 🎛️ Runtime Configuration & Persistence
We believe a good tool should remember your preferences. Project Axis features a lightweight, encrypted `.ini`-style configuration handler. Your settings—such as the hotkey bindings and the ammo replenishment strategy—are saved locally upon exit and reloaded on the next session. No cloud sync, no telemetry, just plain, local interoperability.

### 🛠️ The "Safe Unload" Protocol
Concerned about leaving the mod environment? The trainer includes a dedicated unload routine (`SafeEject`) that restores all intercepted memory vectors to their original state, removes the message hooks, and returns the game to a pristine condition. This is crucial for players who want to preserve their original save files or switch to a different mod environment without reinstalling the game.

## 📦 Repository Structure

```
gtasa-internal-trainer/
├── /src
│   ├── /core           # Main DLL entry point, hook engine, and memory scanner
│   ├── /features       # Individual feature modules (ammo, status, etc.)
│   ├── /ui             # In-game overlay and notification system
│   └── /utils          # String manipulation, logging, and registry access
├── /include            # Public headers for the SDK interface
├── /scripts            # Build scripts and asset compilation automations
├── /docs               # Static documentation and API reference
├── LICENSE             # MIT License
└── README.md           # You are here
```

## 🧰 Technical Stack & Requirements

- **Language**: C++ (C++17 standard) with a focus on raw memory pointer arithmetic.
- **Build System**: Visual Studio 2019/2022 solution format (`/build/GTASA_Trainer.sln`).
- **Target Platform**: Windows 7 SP1 through Windows 11 (x86/x64 compatibility layer for the game's 32-bit process).
- **Game Version**: GTA San Andreas v1.01 (US Language Pack) only. Does not support the Steam OS version or the mobile ports.

## 📋 Installation & Integration

This is a *developer-centric* tool. Follow these high-level steps to get the module loaded into your game environment:

1. **Obtain the Compiled Binary**: Use a compatible C++ compiler to build the solution in "Release" configuration. The output will be a single `.dll` file.
2. **Inject the Module**: Use a generic process injection utility (such as a standard DLL injector) to load the `.dll` into the running `gta_sa.exe` process. Alternatively, configure a load-on-launch feature in your mod manager.
3. **Trust the Firewall**: The trainer does not access the network. Ignore any false positives from antivirus software that flags DLL injection heuristics.
4. **Default Hotkey**: The `NUM_ADD` key toggles the ammo replenishment on/off. You can change the key binding in the generated configuration file.

> **Note**: We do not encourage circumventing game protections or online multiplayer usage. This project is intended for **offline, single-player** sessions only.

## 🧪 Testing & Quality Assurance

Every release candidate is subjected to a suite of manual test passes covering:
- **Longevity Stress Test**: 12-hour continuous run to check for memory leaks and latency build-up.
- **Cutscene Interaction**: Verifying that the trainer doesn't accidentally trigger during forced camera movements.
- **Mission Integrity**: Ensuring that script-triggered ammo pickups and weapon degradation still function normally when the trainer is idle.
- **Clean Exit**: Confirming that SaveGame files are not modified and the game process exits with zero error codes.

## 🆘 Support & Contribution Guidelines

We welcome contributions that align with our "surgical instrument" philosophy. Before submitting a pull request, please:

- **Read the CONTRIBUTING.md** – We have strict code style rules (tabs, not spaces; braces on new lines).
- **Test your changes** – Provide a brief description of the game scenario you used for testing.
- **Use the Issue Tracker** – For bug reports, please include your build number, game version, and the exact steps to reproduce the crash (if any).

**24/7 Maintenance**: While we can't offer live support, we monitor the issue tracker daily and typically respond within 48 hours. We provide language support in English, Spanish, and Portuguese.

## 🔒 Disclaimer & Ethical Usage

**Important Legal & Ethical Notice**: This software is provided for *educational and research purposes* only. It is a demonstration of memory management techniques in legacy game engines.

We do not condone the usage of this tool in any multiplayer environment, in online sessions, or on any modified server infrastructure where it violates the terms of service. The use of this tool for cheating, griefing, or any activity that disrupts the gaming community is strictly prohibited.

By using this tool, you agree to hold the developers harmless against any game crashes, corrupted save files, or account bans that may result from misuse. The GTA San Andreas logo and game assets are property of Take-Two Interactive, and this project is not affiliated with or endorsed by them.

## 📄 License

This project is released under the **MIT License**. You are free to use, modify, and distribute this software, provided you retain the original copyright notice. We encourage you to share your own modifications back to the community.

```
MIT License

Copyright (c) 2026 Project Axis Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

[View the License](LICENSE)

---

**Final Thoughts**: Project Axis is not just a tool; it's an exploration of how far you can push a two-decade-old game engine with modern, disciplined engineering. The elegance lies in the restraint—we only add what is necessary, and we polish what we add. If you appreciate craftsmanship in code and want a reliable companion for your San Andreas play-through, this repository is your gateway. Dive into the `/src` folder, follow the breadcrumbs, and see how the magic works under the hood. Happy exploring, pilot. 🎮