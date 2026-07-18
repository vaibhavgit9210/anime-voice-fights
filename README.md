# Spatiotemporal Ballistic Manifold

Two silhouettes. One shot. The head doesn't splatter — it **resolves into data**:
40 "cranial frequency coefficients" condensed by PCA into three principal
dimensions, rendered as a drifting point-cloud manifold of boxed nodes, numeric
readouts, and link-line webs.

**Live:** https://vaibhavgit9210.github.io/anime-voice-fights/

A homage to [Lucio Arese's *Visualizing Bird Songs: A Mathematical Model*](https://www.youtube.com/watch?v=cPFmcVtGnh0),
where birdsong MFCCs become spatial acoustic manifolds — except here the
"recording" is considerably more terminal.

## How it works

Single self-contained `index.html` — no build step, no dependencies, canvas 2D.

- **Choreography** (~17s loop): standoff → arm raise → muzzle flash + tracer →
  the victim's head bursts into ~240 particles that damp out of their ballistic
  burst and self-organize onto a clustered 3D manifold (spring-to-target +
  sinusoidal drift), while the camera pushes in and the cloud slowly rotates.
- **The look**: additive-blended boxed nodes with 4-decimal value labels, hue
  clustered by region (green → yellow → orange → red, white anchors with
  sub-readouts), proximity link-lines recomputed every few frames, a white
  trajectory polyline through the anchor nodes, and heavy red droplets that
  fall under gravity and stain the ground with their own readouts.
- **HUD**: impact spread / cranial centroid tickers, emission-time scrubber,
  a 40-row CFC bar stack, and an italic specimen caption —
  *Subject B (Homo Sapiens)*.
- **Sound** (toggle, bottom-right): synthesized WebAudio — filtered-noise
  gunshot with canyon echo delay, sub thump, detuned drone pad, data blips.

## Test hooks (headless screenshots)

- `?test` — seeded RNG, deterministic run
- `?test&t=<sec>` — jump to a point in the loop; physics is pre-integrated so
  the manifold state matches real playback

```bash
"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" \
  --headless=new --disable-gpu --window-size=1280,800 \
  --virtual-time-budget=800 --screenshot=shot.png \
  "file:///path/to/index.html?test&t=9"
```

Click anywhere to replay.
