# Hydra Sketches

Audio-reactive visuals for the [Hydra](https://hydra.ojack.xyz/) live-coding video synth.

Each file is a self-contained Hydra sketch. They take the screen as an input (`s0.initScreen()`), run it through oscillators, kaleidoscope, threshold and colorama, and output to the default buffer.

## Sketches

- **LSD Snow**: layered kaleidoscope with screen feedback and thresholded colorama.
- **Mandala Blooms**: mandala-style bloom using additive blends and repeated kaleidoscope symmetry.
- **Starfield**: starfield-like feedback with layered rotation and color cycling.

## Running a sketch

1. Open [hydra.ojack.xyz](https://hydra.ojack.xyz/) in a browser.
2. Paste the contents of a sketch file into the editor.
3. Press `Ctrl + Enter` to evaluate.

## Requirements

- A browser with WebGL.
- Hydra needs camera/screen capture permission if the sketch uses `s0.initScreen()` or `s0.initCam()`.

## License

MIT
