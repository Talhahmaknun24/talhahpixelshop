# TalhahPixelShop

Tamaddun's free photo editor for the web — a Tamaddun-branded build of
[PhotoCraft](https://github.com/storytold/photocraft) v0.23.1
(MIT OR Apache-2.0), with the Tamaddun light theme (sky blue `#1B9BD8` +
lime-yellow `#DCE625`), a glass-effect loading screen, and the Tamaddun logo.

Live site: deployed from this repo on Vercel.

## How this repo is built

This repo holds the prebuilt static site (no build step needed):

- `index.html` — page + loader (Tamaddun logo inlined as a data URI)
- `photocraft-web-*.js` — wasm-bindgen glue
- `snippets/eframe-*/inline0.js` — eframe text-agent snippet
- `wasm/part0.b64` … `wasm/part6.b64` — the 74 MB WebAssembly file, split
  into 7 base64 text chunks

Why the chunks: the GitHub connector used to publish this site only accepts
UTF-8 text files (max 16 MiB per push), so the `.wasm` binary is stored as
base64 text and reassembled in the browser by the loader in `index.html`
(fetch → `atob` → `Blob` → `init({ module_or_path: blobUrl })`). The
reassembled bytes are verified identical to the built wasm
(sha256 `ab5f1317fa0ab4a54fa58b3ea525121ca6736f1efbcd159767eeaa5440261355`).
To update the app, rebuild the web bundle and replace the chunks + glue
files; the loader stays the same.

## Attribution

PhotoCraft is © storytold / ArtCraft contributors, dual-licensed
MIT OR Apache-2.0 (see `LICENSE-MIT` / `LICENSE-APACHE` in the
[PhotoCraft repo](https://github.com/storytold/photocraft)). This build
renames the app to TalhahPixelShop and applies Tamaddun branding, as the
PhotoCraft brand licence requires forks to remove the ArtCraft name and
wordmark.
