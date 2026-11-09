# rvmm-zygisk-mount (v12 Fix)

Injects the mounts at pre-app specialization with Zygisk (for [revanced-magisk-module](https://github.com/j-hc/revanced-magisk-module)).

This fork includes critical bug fixes for issues where apps (such as YouTube Music, Google Photos, etc.) lost their mounts on reboot and required manual re-flashing or triggering action scripts.

### What's Fixed in v12:
- **Reboot Persistence Fix:** Fixed shell service crashing on boot due to uninitialized `${MODPATH:?}` variable, ensuring `procs_map` is properly created and updated at every boot.
- **Immediate First-Boot Setup:** Ensures `procs_map` is written during installation directly into the module directory.
- **Companion Memory Safety (Use-After-Free):** Fixed a critical use-after-free bug in Zygisk companion where mount paths were freed before mounting, causing permission/access denied errors under Scudo allocator.
- **Split APK Support:** Properly handles split APK paths returned by `pm path`, preventing string corruption in the mount map.
- **SELinux Enforcement:** Automatically sets `u:object_r:apk_data_file:s0` context on patched APKs and map files.
- **KernelSU Next Compatibility:** Dynamic profile handling and universal support across KernelSU Next, APatch, and Magisk.

## Usage
- Make sure your patched module from revanced-magisk-module is installed.
- Flash `rvmm-zygisk-mount-v12.zip` in your root manager (KernelSU / APatch / Magisk).
- **Do not** put the patched apps in the denylist / unmount list.
- Reboot and enjoy persistent mounts without manual intervention.
