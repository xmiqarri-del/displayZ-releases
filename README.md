# G700 Releases 🚗⚡

The official distribution point for the G700 app family — every signed APK your car or your phone ever installs comes from here.

🚘 **Car Android G700** — the in-car head-unit app
- Tagged `car-v<version>` per release (e.g. `car-v1.1.38`), plus `car-latest` — a pointer that always follows the newest one.

📱 **G700 RemoteZ** — the phone-side BLE remote
- Tagged `remote-v<version>` per release (e.g. `remote-v0.7.2`), plus `remote-latest` — same deal.

`<version>` isn't a live placeholder — it's just shorthand for "whatever version that release is." Each new release gets its own fixed tag; the `*-latest` tags are the only ones that move. They each hold a tiny `update.json` pointing at the matching `*-v<version>` release, so the APK itself is uploaded **once per version**, never re-uploaded on every sync.

## 🔒 Why this repo exists

The real source code for both apps lives in private repositories. This repo holds **only the built, signed artifacts**, so the in-app auto-updaters and the [Web Installer](https://github.com/xmiqarri-del/Web-Installer) can fetch new releases over HTTPS — no authentication token required.
