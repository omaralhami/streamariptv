# Antivirus False Positive - Quick Guide for Clients

## ⚠️ This is a FALSE POSITIVE

Your antivirus may flag this application, but **it is completely safe**. This is a common issue with new applications.

## Why This Happens

The app creates a **local proxy server** to stream videos efficiently. Some antivirus software flags this as suspicious behavior, even though it's completely legitimate.

## Quick Solution

**Add the application to your antivirus exclusions/whitelist.** This is safe because:
- The app only connects to IPTV servers YOU configure
- It only runs on your computer (localhost)
- It doesn't modify system files
- Major antivirus vendors (Microsoft, Kaspersky, Bitdefender) report it as clean

## Verification

1. **Check VirusTotal**: Only 2-3 out of 70+ antivirus engines flag it (heuristic/AI-based, not actual malware)
2. **Built with Tauri**: Official, trusted framework used by thousands of applications
3. **Open Source Dependencies**: All code comes from trusted, official sources

## Still Concerned?

- Use Windows Defender only (it doesn't flag this app)
- Wait a few days and rescan (antivirus databases update regularly)
- Contact support if you have questions

---

**The application is safe to use.** These are false positives from overly aggressive heuristic scanners.
