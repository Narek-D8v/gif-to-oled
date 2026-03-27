# 🚀 OLED GIF Converter
_**This is a simple, browser-based tool designed for ESP32 and Arduino enthusiasts. It allows you to convert any GIF animation into a C++ compatible array format to display animations on SSD1306 128x64 OLED screens.**_

# ✨ Features
### Auto-Scaling: Automatically resizes any GIF to 128x64 pixels.

### Monochrome Conversion: Uses a brightness threshold to turn frames into high-contrast black & white pixels.

### Animation Support: Decompresses GIF frames and converts them into a 2D array (animation_frames[frame_count][1024]).

### PROGMEM Ready: Generates code that stores data in Flash memory to save RAM on your microcontroller.

### Instant Preview: See how your GIF will look on the OLED display before uploading the code.

# 🛠 How to Use
## Open the [GitHub Pages](https://pages.github.com/).

### Upload your .gif file.

### Wait for the frames to process.

### Copy the generated code from the text area.

### Paste it into your Arduino sketch and use display.drawBitmap() to play the animation.

# 📦 Built With
### gifuct-js — GIF decompression.

### Pure JavaScript & HTML5 Canvas.
