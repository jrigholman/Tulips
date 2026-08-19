# Tulips 🌷

One flower, blooming around Amy's name on black — a single self-contained web
page (real-time raymarched WebGL2, embedded fonts, no external requests).

**A different flower every visit.** One parameterised bloom drives 13 species
across four petal architectures, so each time she opens the link she gets a
different flower — and never the same one twice in a row.

| Architecture | Species |
|---|---|
| dense spiral | garden rose, peony, dahlia, ranunculus |
| few sculptural petals | tulip, lily, magnolia |
| flat radiating rays | lotus, water lily, chrysanthemum |
| simple five | cherry blossom, cosmos, anemone |

Petal count, whorls, length, width, curl, cup, ruffle, tip sharpness and colour
are all jittered per visit on top of the species preset, so even a repeat
species is never quite the same bloom.

## Deploy with GitHub Pages

1. **Settings → Pages → Build and deployment**
2. Source: **Deploy from a branch**
3. Branch: **main**, folder **/ (root)** → Save

A minute or two later it is live at **https://jrigholman.github.io/Tulips/**
(and at the custom domain in `CNAME`).

## URL parameters

| Param | Effect |
|---|---|
| `?for=NAME` | Tags the visit for analytics, and names the recipient in the phone buzz |
| `?f=0..12` | Force a specific species (index into the table above) |
| `?t=SECONDS` | Jump to a point in the bloom timeline (negative values show the closed bud) |
| `?debug=1` | On-screen readout: species, frame time, quality tier, canvas size, GPU |
| `?q=0..6` | Force a quality tier and disable adaptive scaling |
| `?mute=1` / `?unmute=1` | Silence / re-enable notifications on this device |
| `?check=1` | Show a "notify sent ✓ / FAILED ✗" toast |
| `?still=1` | Render one frame and stop; also suppresses notifications |

## Personalize

The name lives in `#name` and in the fallback section of `index.html`. It is
placed at the exact centre of the frame, which is where the shader aims the
camera — the heart of the bloom — so it cannot drift out of sync.
