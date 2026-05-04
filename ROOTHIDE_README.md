# Dopamine with Roothide Integration

This is an enhanced version of Dopamine with full Roothide integration for iOS 15-16.

## ✨ New Features

### 🔒 Roothide XPC Domain (Domain #5)
- Dedicated XPC communication channel for roothide-specific functionality
- Improved security through domain-based access control
- Per-process configuration support

### 🛡️ Jailbreak Detection API
- `jbclient_roothide_jailbroken()` - Query jailbreak status
- `jbclient_palehide_present()` - Detect palera1n hidden mode
- Applications can now properly detect jailbreak status

### 📱 Process Blacklist System
- Filter sensitive applications (banking, security, anti-cheat)
- Three check types: PID, path, bundle identifier
- Dynamic blacklist updates

### ⚙️ dyld-Patch Per-Process Control
- Get/set dyld patch enabled state per process
- iOS 15 arm64e spinlock fix support
- Better compatibility with complex apps

### 🗂️ Path Virtualization
- `@loader_path/.jbroot` prefix support
- Transparent mapping to `/var/jb` directory
- Hides jailbreak binaries from introspection

### 🤝 palera1n Compatibility
- Detect palera1n "hide" mode
- Multi-jailbreak support
- Better ecosystem integration

## 📋 Supported iOS Versions

| iOS Version | arm64 | arm64e | Status |
|-------------|-------|--------|--------|
| iOS 15.0-15.8 | ✅ | ⚠️ (Spinlock) | Supported |
| iOS 15.8.1-15.8.6 | ✅ | ✅ | Full Support |
| iOS 16.0-16.6.1 | ✅ | ✅ | Full Support |

## 🔧 Building

### Prerequisites
- macOS 12+
- Xcode
- Theos
- Procursus Tools
- iPhoneOS16.5.sdk

### Build
```bash
cd Mofarthim/Dopamine
gmake -j$(sysctl -n hw.physicalcpu)
```

### Output
- `Application/Dopamine.tipa` - Ready to install

## 🚀 Installation

### Using Dopamine App (Recommended)
1. Download `dopamine-roothide-*.tipa`
2. Open in Dopamine app
3. Install

### Manual Installation
```bash
scp Application/Dopamine.tipa user@device:/var/mobile/Documents/
ssh user@device "cd /var/mobile/Documents && unzip -q Dopamine.tipa && rm Dopamine.tipa"
```

## 📚 API Usage

### Check Jailbreak Status
```c
#include <libjailbreak/jbclient_roothide.h>

bool is_jailbroken = jbclient_roothide_jailbroken();
if (is_jailbroken) {
    NSLog(@"Device is jailbroken");
}
```

### Check Process Blacklist
```c
bool is_blacklisted = jbclient_blacklist_check_bundle("com.example.app");
if (!is_blacklisted) {
    // Safe to proceed
}
```

### Control dyld Patch
```c
bool patch_enabled = jbclient_dyld_patch_enabled();
jbclient_set_dyld_patch(true);  // Enable
```

## 🔍 Debugging

### Enable Logging
Set environment variable:
```bash
export ENABLE_LOGS=1
```

### Monitor jailbreakd
```bash
sudo log stream --predicate 'process == "jailbreakd"' --level debug
```

## 🤝 Contributing

This is a fork combining:
- **opa334/Dopamine** - Original jailbreak
- **roothide/Dopamine2-roothide** - Roothide enhancements

See `ROOTHIDE_INTEGRATION_GUIDE.md` for detailed technical information.

## 📄 License

MIT License - See LICENSE.md

## ⚠️ Disclaimer

This tool is provided for educational and authorized testing purposes only. Unauthorized access to computer systems is illegal.

---

**Build Version:** See GitHub Releases
**Last Updated:** $(date)
