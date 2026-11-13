# Hydra Sketches

Livecoding sketches for the Hydra video synth.

**Try it in your browser:** [Open the Hydra editor](https://hydra.ojack.xyz/) and paste in a sketch.

## What this is

[Hydra](https://hydra.ojack.xyz/) is a video synthesiser that runs in a web browser. Like a music synth, it chains small building blocks together, but its blocks make and change images. Livecoding means writing and changing the code while the visuals are running.

Each file here is a Hydra sketch: a few dozen lines of JavaScript that take a picture of your screen as input and fold it into moving kaleidoscope patterns. The output changes all the time, and it changes again with whatever is on your screen.

Caution: these sketches make fast-changing, high-contrast patterns. If flashing images affect you, do not run them.

## What you can learn from it

- How a chain of functions builds a result step by step, where each step takes the last one's output (Computer Science).
- How feedback works: the sketch shows your screen, which shows the sketch, which shows your screen (Computer Science, Physics).
- How sine and cosine of time make values that rise and fall smoothly, used here to animate colour and symmetry (Mathematics).
- How kaleidoscopes use reflection and rotation to make symmetry (Mathematics, Art and Design).
- How a threshold turns a smooth image into hard black and white shapes (Computer Science, Art and Design).

## Run it

### In your browser

**You will need:** a computer with a recent browser that supports WebGL (the system browsers use for 3D graphics). Hydra's own README says it works best in Chrome or Chromium. Phones and tablets cannot share their screen this way.

1. Open one of the sketch files on GitHub, for example **Starfield**, and copy all of its text.
2. [Open the Hydra editor](https://hydra.ojack.xyz/). It starts with an example sketch already running.
3. Click in the code, select all of it and delete it.
4. Paste the sketch.
5. Press Ctrl, Shift and Enter together to run all the code.
6. Your browser asks which screen, window or tab to share. Pick one. The sketch uses it as its input.

You should see a kaleidoscope pattern built from the screen you chose, changing colour over time.

**LSD Snow** and **Mandala Blooms** each hold two versions, separated by a line of slashes. Running the whole file is fine, and the second version replaces the first. To see the first version, paste only the part above the slashes.

### Hydra editor keys

These come from [Hydra's README](https://github.com/hydra-synth/hydra).

| Keys | What they do |
|---|---|
| Ctrl + Enter | Run the line the cursor is on |
| Ctrl + Shift + Enter | Run all the code on screen |
| Alt + Enter | Run the block the cursor is in |
| Ctrl + Shift + H | Hide or show the code |
| Ctrl + Shift + F | Tidy the code layout |
| Ctrl + Shift + S | Save a screenshot |

## How it works

A Hydra sketch is one long chain. Each dot adds a step that changes the image coming from the step before it.

All three sketches follow the same plan:

1. `s0.initScreen()` captures your screen into a source called `s0`.
2. `src(s0)` starts the chain with that screen image.
3. `.blend(osc())` mixes in `osc()`, a pattern of moving stripes.
4. `.rotate(...)` and `.kaleid(...)` turn the image and fold it into a kaleidoscope. The number of kaleidoscope sides is a function of `time`, so it keeps changing.
5. A second copy of the same chain is combined with the first, using `.layer` or `.add` or `.blend`.
6. `.colorama()` shifts the colours, `.thresh(...)` cuts the image into hard shapes, and `.repeat(...)` tiles it.
7. `.out()` sends the result to the screen.

Code written as `({time}) => ...` is a small function. Hydra runs it again for every frame, so the value changes as time passes.

| File | What is in it |
|---|---|
| `LSD Snow` | Two versions of a layered kaleidoscope with screen feedback and thresholded colorama |
| `Mandala Blooms` | Two mandala-style blooms using additive blends and repeated kaleidoscope symmetry |
| `Starfield` | Starfield-like feedback with layered rotation and colour cycling |

The files have no file extension. They are plain text with JavaScript inside.

## Ideas to try

1. In `Starfield`, change the `20` in `.kaleid(20)` near the end to a small number such as `4`, and run it again.
2. In `LSD Snow`, change the number in `.thresh(0.3)`. Values near 0 give mostly white, values near 1 mostly black.
3. In any sketch, replace `s0.initScreen()` with `s0.initCam()` to use your webcam as the input.
4. In `Mandala Blooms`, swap `.add(` for `.diff(` and see how the two layers combine.
5. Make it react to sound. Hydra can listen to the microphone through `a.fft`. In `Starfield`, replace the `0.3` in `.thresh(0.3)` with `() => a.fft[0]`. The [Hydra function reference](https://hydra.ojack.xyz/api/) lists the other functions.

## Technical details

Each file is a self-contained Hydra sketch. They take the screen as an input (`s0.initScreen()`), run it through oscillators, kaleidoscope, threshold and colorama, and output to the default buffer.

The kaleidoscope side count in each chain is `Math.pow(Math.log(((sin(t)+1)^2 / (cos(t)+1)) / 10000), 2)` with `t` equal to `time` or `time/2`. `Mandala Blooms` #2 divides by 20000 in its second chain.

In `Starfield`, `.repeat(Math.sin(time),3,3)` is not wrapped in a function, so `Math.sin(time)` is read once when the code runs and stays fixed.

Hydra needs camera or screen capture permission when a sketch uses `s0.initScreen()` or `s0.initCam()`.

## Project status

These are finished sketches with no tests. None of the three reads audio input. They react to whatever is on the captured screen.

## Licence

You can use, copy and change these sketches for any purpose, as long as you keep the copyright notice. See [LICENSE](LICENSE) (MIT). Hydra itself has its own licence.

## Credits

Written by Abhishek Shivakumar. Built for [Hydra](https://github.com/hydra-synth/hydra) by Olivia Jack and contributors. To cite this work, see [CITATION.cff](CITATION.cff).
