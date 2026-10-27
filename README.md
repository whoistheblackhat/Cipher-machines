# Cipher-machines

Static browser VM assets for CipherPoint Cipher Day 01. The VM runs in each
learner's browser; this repository is deployed as a Render Static Site only to
serve its public files.

## Deploy on Render

1. Push this repository to GitHub.
2. In Render, create **New → Static Site** and connect this repository.
3. Use the `main` branch, leave **Root Directory** empty, set **Publish
   Directory** to `public`, and set the build command to `echo "No build
   required"`.
4. After the site is created, open its **Headers** settings and add:
   - Path: `/*`
   - Name: `Access-Control-Allow-Origin`
   - Value: `*`
5. After deploy, check that these URLs load:
   - `/v86/build/libv86.js`
   - `/v86/build/v86.wasm`
   - `/images/cipher-day-fs.json`
   - `/images/cipher-day-rootfs-flat/` followed by a chunk filename

The files are public and contain no user data, so wildcard CORS is appropriate.
Set Botkeep's `CIPHER_DAY_ASSET_BASE_URL` to the Render site's origin, for
example `https://cipher-machines.onrender.com` (do not append `/public`).

## Contents

- `public/v86/`: v86 browser runtime and BIOS files.
- `public/images/cipher-day-fs.json`: filesystem manifest.
- `public/images/cipher-day-rootfs-flat/`: compressed filesystem chunks.

Only runtime files are included. The approximately 474 MB
`cipher-day-rootfs.tar` is a build intermediate and must not be uploaded. The
runtime payload is about 167 MB across the chunk files and emulator assets.
Expect a first-time learner download of roughly this size; monitor Render
bandwidth usage as participation grows.
