# X-NIX Web Installer (standalone, rebranded)

WebUSB browser flasher for X-NIX, derived from the GrapheneOS web installer
(forked from GrapheneOS/grapheneos.org + GrapheneOS/fastboot.js).

## What was changed from upstream
- `js/web-install.js`: RELEASES_URL -> https://ota.foxnet.live ; brand strings -> X-NIX ;
  fastboot import path -> ./fastboot/fastboot.min.mjs
- `index.html`: standalone page (build macros/jinja removed), rebranded GrapheneOS -> X-NIX,
  added unverified-image warning banner, dark purple X-NIX theme.
- Engine `js/fastboot/fastboot.min.mjs` (+ vendor pako worker) vendored from upstream unchanged.

## Deployment
Served by Caddy at https://flash.foxnet.live (root = this dist/). It fetches the signed
factory/install zip + channel metadata from https://ota.foxnet.live (the OTA server), which
sends CORS/CORP headers permitting the cross-origin download.

## Device support
Currently gated to mustang (Pixel 10 Pro XL), build 2026101600. supportedDevices[] in
web-install.js still lists all upstream Pixels but only mustang has an X-NIX release published.

## SAFETY
The installer's lock-bootloader step is retained. For a FIRST flash of an unproven build, flash
UNLOCKED, boot-test, and only lock after confirming the OS boots. See the banner on the page.
