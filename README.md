# 📟 OLED Media Multitool

**OLED GIF Converter** is a professional browser-based tool designed to transform animated GIFs into C-style byte arrays (HEX). It is specifically optimized for monochrome OLED displays (like **SSD1306**) used in **Arduino**, **ESP32**, and **STM32** projects.

[![Live Demo](https://img.shields.io/badge/Demo-Live%20Website-brightgreen?style=for-the-badge&logo=github)](https://narek-d8v.github.io/gif-to-oled/)

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Language: JavaScript](https://img.shields.io/badge/Language-JavaScript-f7df1e.svg)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[![Deployment: GitHub Pages](https://img.shields.io/badge/Deployment-GitHub%20Pages-222222.svg)](https://pages.github.com/)

---

## 🚀 Live Access

No installation required. Use the tool directly online:
👉 **[https://narek-d8v.github.io/gif-to-oled/](https://narek-d8v.github.io/gif-to-oled/)**

---


## ✨ Features

- **⚡ High-Performance Conversion:** Entirely client-side processing using `Vanilla JS`.
- **🎞 Video & GIF Support (minimal quality loss):**
  - Frames extracted via **FFmpeg.wasm** at high resolution (Lanczos scaling) — no pre-cropping to 128x64, so detail is preserved.
  - A single high-quality (smooth) downscale to the OLED grid happens in-browser.
  - **Original GIF timing preserved** — playback uses the GIF's native frame delays (GCE), not a forced frame rate.
  - **Motion Smoothing (video):** optional `minterpolate` interpolation (2x/4x) constructs smooth in-between frames.
  - **HDR → SDR Tonemap:** optional BT.709 tonemapping for HDR video, with automatic fallback per FFmpeg build.
- **🎨 Advanced Dithering:**
  - **Error Diffusion:** Floyd-Steinberg, Jarvis-Judice-Ninke, Stucki, Atkinson, Burkes, Sierra.
  - **Ordered / Bayer:** 4x4 and 8x8 threshold matrices for a retro-digital look.
  - **Blue Noise:** void-and-cluster ordered dithering (seeded, deterministic) for artifact-free, film-like grain.
  - **Serpentine scanning** reduces directional artifacts in diffusion.
- **🕒 Flicker Reduction:** temporal hysteresis (stable pixels hold their state ±8 gray levels) eliminates flicker on animated content.
- **⚙️ Smart Auto-Tune:** the tool measures on-screen motion and automatically lowers the frame rate for calm video (saving flash space), and auto-detects HDR video to enable tonemapping.
- **💡 Built-in Guidance:** every control has a hover "i" tooltip explaining exactly what it does.
- **🌐 English / Русский:** toggle the UI language in the header (EN/RU); your choice is saved in localStorage and the whole interface, tooltips and log messages switch instantly.
- **🎯 High-Fidelity Pre-Processing:**
  - **Perceptual sRGB luminance** (accurate Rec.601/709 alternatives) for correct color → mono mapping.
  - **Auto-Levels** adaptive contrast stretch (percentile-clipped histogram).
  - **Detail Boost (Unsharp Mask)** to recover edge detail after downscaling.
- **🛠 Precise Controls:**
  - Real-time frame-by-frame preview.
  - Dynamic **Threshold** adjustment (applies to all algorithms).
  - One-click **Inversion** toggle.
  - **Transparent Fill** (black or white) for transparent inputs.
- **📐 Smart Scaling:**
  - **Fit:** Maintain aspect ratio.
  - **Fill:** Cover the entire 128x64 area.
  - **Stretch:** Force exact dimensions.
- **💾 Hardware Optimized:**
  - Generates `PROGMEM` arrays to save precious RAM on Arduino Uno/Nano.
  - Cross-platform guard (AVR / ESP32 / STM32) in the generated header.
  - Supports **MSB First** bit order (standard for Adafruit_SSD1306).
- **🌌 Modern UI:** Dark cyberpunk-inspired theme with smooth animations and JetBrains Mono typography.

---

## 🛠 Usage Guide

1. **Upload:** Drag & drop your GIF or click the upload zone.
2. **Configure:** - Choose your **Dithering** method for the best look.
   - Adjust the **Threshold** slider to catch the right details.
   - Select **Scaling** to fit your screen perfectly.
3. **Generate:** Preview the animation using the frame slider.
4. **Copy:** Click "Copy Code" and paste the array directly into your C++/Arduino project.

---

## 💻 Arduino / ESP32 Code Example

The generated output is ready-to-use with libraries like `Adafruit_SSD1306` or `U8g2`:

```cpp
// Example of generated output (2D array, works on AVR / ESP32 / STM32)
const uint8_t oled_animation_data[8][1024] oled_animation_PROGMEM = {
    { 0x00, 0x18, 0x3C, 0x7E, 0xFF, 0x7E, 0x3C, 0x18, ... },
    ...
};

// Usage with Adafruit_SSD1306:
display.drawBitmap(0, 0, oled_animation_data[frame_index], 128, 64, WHITE);
display.display();
