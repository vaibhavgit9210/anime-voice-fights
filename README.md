# Spatiotemporal Vocal Manifold

Speak, and watch your voice unfold as a live mathematical manifold — the
pipeline from [Lucio Arese's *Visualizing Bird Songs: A Mathematical Model*](https://www.youtube.com/watch?v=cPFmcVtGnh0),
running in realtime on **your microphone**.

**Live:** https://vaibhavgit9210.github.io/anime-voice-fights/

## The pipeline (real, not faked)

Single self-contained `index.html` — no build step, no dependencies, no
servers; audio never leaves the page.

1. **Mic → spectrum.** Web Audio `AnalyserNode`, 2048-point FFT per frame.
2. **40 MFCCs.** A 40-filter mel filterbank (80 Hz – 8 kHz) → log energies →
   DCT-II. Same descriptor family the birdsong video uses.
3. **Streaming normalization.** Exact running mean early, then EMA z-scoring
   per coefficient, clamped for stability.
4. **Online PCA.** Sanger's rule (generalized Hebbian algorithm) learns the
   top 3 principal components *while you speak* — the manifold's axes
   literally self-organize to the structure of your voice.
5. **Emission.** Each voiced frame (RMS gate with hysteresis, ~30 Hz) emits a
   point into the 3D cloud: boxed node, 4-decimal readout, hue clustered by
   manifold region (green → yellow → red), white anchors carrying real
   spectral-centroid/spread sub-readouts. Proximity link-lines weave the web;
   a bright white trajectory traces your last ~26 emissions in order; the
   whole cloud slowly rotates. Oldest points fade once the cloud is full.

HUD values are real too: spectral spread + centroid (kHz, red activity box
while you're voiced), and 40 live MFCC magnitude bars. Caption:
*Subject A (Homo Sapiens)* — you.

No mic / permission denied? It falls back to a synthetic phoneme-hopping demo
signal (labeled `DEMO SIGNAL (NO MIC)` in the HUD).

## V0 · ballistic build

The first version lives at [`legacy/`](https://vaibhavgit9210.github.io/anime-voice-fights/legacy/):
two silhouettes, one gunshot, and the victim's head resolves into the same
manifold vocabulary (a fixed, choreographed cloud — *Subject B*). Kept as an
honest changelog.

## 360° orbit export

**⏺ EXPORT 360° ORBIT** (bottom-right, once running) drives the manifold
through exactly one horizontal revolution over 8 s while `MediaRecorder`
films the canvas — video only, no audio, so the "nothing is recorded"
promise holds. mp4 (H.264) where the browser can record it — the format
WhatsApp / Instagram / the iOS gallery play natively — else webm. The
rotation hands back to the ambient drift with no visible jump, and the
exported frames carry the site URL bottom-left.

## Test hooks (headless screenshots)

- `?test` — seeded, auto-starts with the synthetic voice (no mic prompt)
- `?test&t=<sec>` — pre-runs the full DSP/PCA/emission pipeline to that time

```bash
"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" \
  --headless=new --disable-gpu --window-size=1280,800 \
  --virtual-time-budget=800 --screenshot=shot.png \
  "file:///path/to/index.html?test&t=45"
```

Same hooks work on `legacy/index.html` (physics pre-integration instead).
