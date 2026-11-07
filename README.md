# Strip Studio: Bluetooth RGB LED controller

A phone web app (installable PWA) that replaces duoCo Strip / Lotus Lamp / Happy Lighting for cheap Bluetooth RGB strips.

## Supported controllers
Command formats for MELK-Ox come from the open-source [elkbledom](https://github.com/dave-code-ruiz/elkbledom) Home Assistant integration.

| Family | Typical device names | BLE service / characteristic | Sold with app |
|---|---|---|---|
| MELK-Ox | `MELK-OA10`, `MELK-OC10`, `MELK-OF10`, `MELK-OG10` | `FFF0` / `FFF3` + login `7e 07 83`, `7e 04 04` | Lotus Lamp X |
| ELK-BLEDOM | `ELK-BLEDOM`, `ELK-BLEDOB`, `MELK`, `LEDBLE` | `FFF0` / `FFF3` | duoCo Strip, Lotus Lamp X, Lantern |
| Triones | `Triones-…`, `QHM-…` | `FFD5` / `FFD9` | Happy Lighting |
| LEDBlue (old Magic Home BLE) | `LEDBlue-…` | `FFE5` / `FFE9` | Magic Home (older) |

The app detects the family when it connects. Other controllers can be added with one entry in the `PROTOCOLS` table in `index.html`.

## Features
- Colour picker, RGB sliders, quick swatches, mixed white temperature
- 9 phone-run effects (Fade, Jump, Breathe, Strobe, Rainbow, Candle, Police, Heartbeat, Sequence) using your own colour steps with per-step fade and hold times, plus 9 palettes
- The controller's built-in modes (these keep running when the app is closed)
- Music sync from the phone mic: Pulse, Spectrum, Hue drift, Beat flash, Bass only
- Image → palette, Image → light timeline, Text → Morse or colour-per-letter
- Saved scenes plus built-ins, with JSON backup and import
- Schedules (on, off, sunrise fade-in, wind-down fade-out, any scene), sleep timer, keep-screen-awake
- Auto-reconnect, demo mode, raw hex console, log

## Run it on your phone (≈5 minutes, free)
Web Bluetooth only works over **https**, so host the folder:

**GitHub Pages**
1. Create a new repo (e.g. `strip-studio`) and upload every file in this folder, keeping `icons/`.
2. Repo → Settings → Pages → Source: *Deploy from a branch* → `main` / root → Save.
3. Open `https://<your-username>.github.io/strip-studio/` in **Chrome on Android**.
4. Chrome menu → **Add to Home screen / Install app**.

**Or Netlify Drop**: drag the folder onto https://app.netlify.com/drop.

Before connecting, **force-close duoCo / Lotus Lamp** (the strip accepts one connection at a time) and turn on Bluetooth and Location.

## Limits
- iPhone Safari has no Web Bluetooth. Use the **Bluefy** browser on iOS.
- A web page stops when the screen turns off. Phone-run effects, music, schedules and the sleep timer need the page open (use "Keep screen awake"). The controller's built-in modes keep running on their own.
- Non-addressable strips show one colour at a time, so they can't draw pictures or scroll text. That needs a WS2812B strip or matrix on an ESP32 (WLED).

## Updating
After editing `index.html`, change `VERSION` in `sw.js` so installed copies pick up the change.
