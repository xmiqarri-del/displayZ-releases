# Steps to Resolve the Network Outage Caused by a Stuck Proxy

## Overview

This document describes how to verify a stuck global proxy on an Android device, remove it safely, and roll back if necessary.

> **Warning:** The root cause stated in the first report (that Car Net G700 is what caused the damage) is **unconfirmed**. The app is only a suspect. The steps below rely on evidence that appears on the device itself.

## Requirements

- An Android device with **Termux**.
- **Shizuku** enabled, and the **rish** tool copied into the Termux folder.
- (Optional) An **adb** connection from a computer to check the state from outside.

## General Order

| Step | Goal | Requires |
|---|---|---|
| 0 | Enter the rish shell | Termux + Shizuku |
| 1 | Check the current state | rish |
| 2 | Back up the settings | rish |
| 3 | Delete the proxy settings | rish |
| 4 | Verify after deletion | rish |
| 5 | Reload the network stack (optional) | rish |
| 6 | Disable the suspect app if the problem persists | rish |
| 7 | Reset network settings (last resort) | Safe Mode |

---

## Step 0: Enter the rish Shell

```bash
cd ~
./rish
```

Make sure the prompt has changed to `rish` before running any delete command.

## Step 1: Check the Current State

Run these commands **before** deleting anything:

```bash
settings get global http_proxy
settings get global global_http_proxy_host
settings get global global_http_proxy_port
settings get global global_http_proxy_exclusion_list
settings get global global_proxy_pac_url
```

- If they are all `null` or `:0`, there is no global proxy and no need to delete. Go to Step 6.
- If any of them have values, continue to Step 2.

## Step 2: Back Up

```bash
settings list global > /sdcard/proxy_backup_global.txt
```

This file lets you restore the values later if you need them.

## Step 3: Delete the Proxy Settings

Run each line separately:

```bash
settings delete global global_http_proxy_host
settings delete global global_http_proxy_port
settings delete global global_http_proxy_exclusion_list
settings delete global global_proxy_pac_url
settings delete global http_proxy
```

## Step 4: Verify After Deletion

Run the Step 1 commands again. **Expected:** `null` on every line.

- If the same values come back, another source is rewriting the setting (most often a VPN app or a device management policy). Go to Step 6.
- If the values are still `null` but the internet is still down, continue to Step 5.

## Step 5: Reload the Network Stack (Optional)

```bash
cmd connectivity airplane-mode enable
cmd connectivity airplane-mode disable
```

This step may do nothing if the proxy is still being enforced by another source.

## Step 6: Disable the Suspect App

If the outage returns or the values come back, check active VPN and filtering apps. The first one to check is **Car Net G700**.

First, find the package name:

```bash
pm list packages | grep -i carnet
```

Then disable the app **without deleting it**:

```bash
pm disable-user --user 0 <package_name>
```

**To undo:**

```bash
pm enable <package_name>
```

## Step 7: Reset Network Settings (Last Resort)

Do not use this step unless the previous steps have failed.

**Warning:** Resetting network settings erases:
- Saved Wi-Fi network passwords
- Paired Bluetooth devices
- Custom mobile data settings

**How to do it:**
1. Restart the device in **Safe Mode** to prevent external apps from re-enforcing themselves.
2. From Settings: **System → Reset options → Reset Wi-Fi, mobile & Bluetooth**.
3. Restart normally.

> **Note:** It has not been proven that this step is what restored the internet in the original case. The cause may have been deleting the setting or restarting the device.

---

## Closing Criteria

A fix is considered successful only with actual outputs:

- [ ] `settings get global http_proxy` returns `null`
- [ ] Internet connectivity works in practice (a website opens)
- [ ] Connecting to a direct IP address works (for example, `ping 8.8.8.8` from Termux)
- [ ] DNS works (for example, `ping google.com`)

## Notes on Users

- The `pm list users` command lists users. Make sure to check the main user (usually 0).
- **Secure Folder** (user 150) does not appear to the shell, so its settings cannot be checked from here.

## Developer Recommendations

- Restore the default setting values when the app closes.
- Use `try-finally` to ensure cleanup runs even on a crash.
- Provide the user with a restore button inside the app.
- Avoid writing to global system settings unless necessary, and inform the user when you do.

## Command Reference

| Command | Function |
|---|---|
| `settings get global <key>` | Read a value |
| `settings delete global <key>` | Delete a value |
| `settings list global` | List all values |
| `pm list packages` | List packages |
| `pm disable-user --user 0 <pkg>` | Disable an app |
| `pm enable <pkg>` | Re-enable an app |
| `cmd connectivity airplane-mode enable/disable` | Reload the network |
