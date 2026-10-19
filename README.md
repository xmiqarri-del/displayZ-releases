# displayZ-releases

Public release assets only — signed APKs and `update.json` manifests for:

- **car_DisplayZ** — tags `car-v<version>` (immutable, one per release) and `car-latest` (moving pointer the app's updater reads)
- **displayZ-remote** — tags `remote-v<version>` (immutable) and `remote-latest` (moving pointer)

The `*-latest` releases only ever contain a small `update.json` whose `apk_url` points at the matching
immutable `*-v<version>` release, so the APK itself is uploaded once per version, not re-uploaded on
every sync.

Source code for both apps lives in private repos. This repo exists only so in-app auto-updaters and the
[Web-Installer](https://github.com/xmiqarri-del/Web-Installer) can fetch release files without authentication.
