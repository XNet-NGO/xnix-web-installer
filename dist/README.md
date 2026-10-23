# X-NIX Web Installer (standalone, rebranded)

WebUSB browser flasher + CLI install guide for X-NIX, derived from the GrapheneOS web installer
(forked from GrapheneOS/grapheneos.org + GrapheneOS/fastboot.js).

## Pages
- `index.html`            -> https://flash.foxnet.live/            (WebUSB web installer)
- `install/index.html`    -> https://flash.foxnet.live/install/    (install landing)
- `install/cli/index.html`-> https://flash.foxnet.live/install/cli/ (command-line guide, sha256 verify)

## Changes from upstream
- web-install.js: RELEASES_URL -> https://ota.foxnet.live ; brand -> X-NIX ; fastboot import path fixed.
- All pages: build macros/jinja removed (standalone), GrapheneOS -> X-NIX, dark purple theme.
- Community/help links repointed to the public repo https://github.com/XNet-NGO/XNetOS ;
  contact -> admin@foxnet.live ; social share links removed.
- CLI "obtaining factory images": GrapheneOS SSH-signature verification replaced with our real
  method (download factory zip + .sha256 from ota.foxnet.live, verify with `sha256sum -c`).
- Dropped links to pages we don't host (/faq, /usage, mangled subdomains, allowed_signers).
- fastboot engine (js/fastboot/fastboot.min.mjs + vendor pako worker) vendored from upstream unchanged.

## Served by
Caddy on the OTA box (EIP 52.73.146.254). ota.foxnet.live sends CORS/CORP headers so the installer
can fetch release zips cross-origin. Auto-TLS via Let's Encrypt.

## SAFETY
Lock-bootloader step retained. For a FIRST flash of an unproven build: flash UNLOCKED, boot-test,
then lock. See the warning banner on the installer page.
