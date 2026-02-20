# SubWoofer

SubWoofer is a lightweight, front‑end‑only web application that demonstrates how to build a simple
browser‑based **bark detector**.  The app loads a pre‑recorded audio file, performs a quick
frequency analysis in the browser, and displays a visual indicator when the audio contains a
frequency signature that matches a dog bark.

## Features

- **Audio playback** – Uses the native Web Audio API to play a WAV/MP3 file.
- **Real‑time analysis** – A `ScriptProcessorNode` (or `AudioWorklet` if available) performs a
  Fast Fourier Transform (FFT) on the incoming audio.
- **Bark detection** – A small heuristic filters the FFT spectrum for frequencies in the
  typical bark range (≈200 Hz‑2 kHz).  When the energy in that band exceeds a threshold, the
  UI lights up.
- **Minimal bundle** – No external dependencies; all logic lives in `index.html` and the
  bundled `audio-worker.js`.
- **Cross‑browser** – Works in all modern browsers that support the Web Audio API.

## Getting started

```bash
# Clone the repository
git clone https://github.com/your-org/subwoofer.git
cd subwoofer

# Just open the page – no build step required
open index.html   # macOS
# or use a local server
# python -m http.server
```

The application will automatically load `static/bark.wav` from the `static/` directory.
Feel free to replace it with your own audio file.

## Project structure

```
├── index.html          # Entry point with UI and audio setup
├── audio-worker.js     # Web Audio worker that does the FFT and bark detection
├── static/
│   └── bark.wav        # Example audio file
└── README.md
```

## How it works

The core algorithm is straightforward:

1.  Read the audio into an `AudioBuffer`.
2.  Connect an analyser node that performs an FFT on each frame.
3.  Inspect the resulting frequency bins and compute the total energy in the bark range.
4.  If the energy exceeds a predefined threshold, fire a `bark` event.
5.  The UI listens for this event and toggles the visual indicator.

The detector is intentionally simple – it’s meant to illustrate the Web Audio API rather than
provide a production‑grade bark‑detection engine.

## Extending the project

- **Better detection** – Replace the threshold logic with a trained classifier or a more
  sophisticated spectral analysis.
- **Multiple microphones** – Use `navigator.mediaDevices.getUserMedia` to stream live audio.
- **UI polish** – Add animations or a real‑time waveform display.
- **Unit tests** – Add Jest tests for the detection logic.

## License

MIT
