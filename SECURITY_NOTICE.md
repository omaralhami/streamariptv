# Security Notice - False Positive Antivirus Detections

## Why Your Antivirus May Flag This Application

**This is a FALSE POSITIVE.** Your antivirus software may flag this application because:

1. **Local Network Server**: The app creates a local proxy server (on `127.0.0.1:1421`) to stream video content. This is a legitimate feature that allows the app to handle video streaming efficiently, but some antivirus software flags any application that creates network servers.

2. **Network Requests**: The app makes network requests to IPTV providers to fetch content. This is normal behavior for a streaming application, but heuristic-based antivirus scanners may flag it.

3. **Unsigned Executable**: The application is not digitally signed (code signing certificates cost $200-400/year). Unsigned executables are more likely to be flagged by antivirus software.

4. **New/Unknown Application**: Since this is a new application, it's not yet in antivirus whitelists. Machine learning-based scanners (like Trapmine) often flag unknown applications.

## What These Detections Mean

- **W64.AIDetectMalware**: AI/heuristic-based detection that can produce false positives
- **Trapmine Malicious.high.ml.score**: Machine learning model that flags unknown applications
- **Generic detections**: These are not specific malware signatures, but rather "suspicious behavior" flags

## Verification Steps

1. **Check VirusTotal Details**: Look at the "Details" tab on VirusTotal. You'll see that major antivirus vendors (Microsoft Defender, Kaspersky, Bitdefender, etc.) report it as clean.

2. **Source Verification**: This application is built with:
   - Tauri v2 (official framework: https://tauri.app)
   - Rust (systems programming language)
   - React (web framework)
   - All dependencies are from official, trusted sources

3. **Behavior Analysis**: The application only:
   - Connects to IPTV servers you configure
   - Creates a local proxy server for video streaming
   - Stores your credentials securely (encrypted)
   - Does NOT access files outside its own directory
   - Does NOT modify system settings
   - Does NOT communicate with unknown servers

## How to Proceed Safely

### Option 1: Add Exception (Recommended)
1. Add the application folder to your antivirus exclusions/whitelist
2. This is safe because the app only runs locally and connects to servers you configure

### Option 2: Wait for Whitelisting
- Submit a false positive report to the antivirus vendor
- Wait a few days for their database to update
- Rescan the file

### Option 3: Use Windows Defender Only
- Windows Defender (Microsoft's built-in antivirus) does not flag this application
- You can temporarily disable other antivirus software if needed

## Technical Details

**Application Purpose**: IPTV streaming client
**Framework**: Tauri v2 + React + Rust
**Network Behavior**: 
- Creates local HTTP proxy on `127.0.0.1:1421`
- Makes HTTPS/HTTP requests to user-configured IPTV providers
- All network activity is initiated by user actions (playing content)

**File System Access**:
- Only reads/writes to application data directory
- Stores encrypted credentials in user's AppData folder
- No system file modifications

## Contact

If you have concerns, please contact the developer. The source code can be reviewed if needed.

## Report False Positives

If you want to help, you can report false positives to:
- **Bkav**: https://www.bkav.com/support
- **Trapmine**: Contact through their website
- **VirusTotal**: Use the "False Positive" button on the scan results page

---

**Last Updated**: 2025-01-27
**Application Version**: 1.0.0
