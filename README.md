# G700 Releases 🚗⚡

The official distribution point for the G700 app family — every signed APK your car or your phone ever installs comes from here.

| App | What it is | Immutable release | Always-latest pointer |
|---|---|---|---|
| 🚘 **Car Android G700** | The in-car head-unit app | `car-v<version>` | `car-latest` |
| 📱 **G700 RemoteZ** | The phone-side BLE remote | `remote-v<version>` | `remote-latest` |

Each `*-latest` release is just a tiny `update.json` pointing at the matching immutable `*-v<version>` release — the APK itself is uploaded **once per version**, never re-uploaded on every sync.

## 🔒 Why this repo exists

The real source code for both apps lives in private repositories. This repo holds **only the built, signed artifacts**, so the in-app auto-updaters and the [Web Installer](https://github.com/xmiqarri-del/Web-Installer) can fetch new releases over HTTPS — no authentication token required.
