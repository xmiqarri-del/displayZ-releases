# 🚗⚡ Meet the G700 App Ecosystem: Next-Level In-Car Intelligence

Transform your driving experience with the **G700 App Family** — the ultimate, privacy-first ecosystem designed specifically for modern Android car head units and smartphones. Built for performance, security, and seamless vehicle integration, here is a professional overview of what makes the G700 ecosystem a true game-changer:

---

### 🌟 Car Android G700: The Ultimate Head-Unit Powerhouse

Engineered exclusively for Android 11+ car displays, this application brings robust control right to your dashboard with **zero ads, zero tracking, and absolute privacy**.

- **Smart Floating Button & App Grid:** Instantly access your most-used apps, search through categorized chips, and clean up background memory with a single tap.
- **Accessibility-Powered Navigation:** Back, Home and Recents, available over any app, without reading screen content.
- **Rear Passenger Entertainment (Display 5):** Mirror your main screen onto the rear passenger display or launch independent applications, with local ADB touch-forwarding.
- **Intelligent Vehicle Integration & Automated Locks:** Customizable Delayed Lock sequences (flashing hazards, folding mirrors, shutting down screens), automatic state restoration, and Fob-Lock Assist for when the car rejects a key lock while running.
- **Secure Over-The-Air Updates:** Background checks every 6 hours, HTTPS-only, verified against a SHA-256 hash before anything installs.

---

### 📱 G700 RemoteZ: Your Car, Right in Your Pocket

Take control of your vehicle straight from your smartphone.

- **BLE-Powered Companion:** Pair your phone securely over Bluetooth Low Energy, with a one-time code and fingerprint verification on both screens.
- **Remote Control at Your Fingertips:** Read live vehicle metrics, manage rear-screen mirroring, launch permitted apps, and lock or unlock your doors on demand.

---

### 🔒 Frictionless & Secure Distribution Hub (this repo)

Every signed APK both apps ever install comes from here:

- 🚘 **Car Android G700** — tagged `car-v<version>` per release (e.g. `car-v1.1.38`), plus `car-latest`, a pointer that always follows the newest one.
- 📱 **G700 RemoteZ** — tagged `remote-v<version>` per release (e.g. `remote-v0.7.2`), plus `remote-latest`, same deal.

`<version>` isn't a live placeholder — it's shorthand for "whatever version that release is." Each release gets its own fixed tag; only the `*-latest` tags move, each holding a tiny `update.json` that points at the matching `*-v<version>` release, so the APK itself is uploaded **once per version**, never re-uploaded on every sync.

The real source code for both apps lives in private repositories. This repo holds **only the built, signed artifacts**, so in-app auto-updaters and the [Web Installer](https://github.com/xmiqarri-del/Web-Installer) can fetch new releases over HTTPS — no authentication token required.

*Experience the future of smart driving — where safety, advanced technology, and effortless control meet on the open road.*
