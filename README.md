# Tulips 🌷

One flower, blooming around Amy's name on black.

There are two ways it can draw that flower, and it picks the best one available:

1. **A filmed bloom** — a random clip from `flowers/`, if one is there and loads.
2. **A procedural bloom** — a real-time raymarched WebGL2 flower, if no clip is
   available, the connection is too slow, or autoplay is blocked.
3. **A still** — her name and an emoji, if there is no WebGL2 either.

Each rung falls through to the next on its own, so `flowers/` can be empty (or
half full) and the page still works. See `flowers/README.md` to add clips.

**One flower per day.** Every time she opens the link on a given day she gets
the same flower; the next day she opens it, she gets the next one along.

The rotation steps forward per *new day* rather than keying straight off the
date, so she walks the whole set in order even if she skips days — she never
misses a flower. The day rolls over at **her own local midnight**, not UTC,
which matters because she is hours ahead. With no stored state (cleared
storage, private browsing, a new device) it falls back to deriving the index
from the date itself, so it still varies and still holds for a whole day.

The procedural bloom's shape and colour jitter is seeded from the day too, so
her morning look and her evening look are the identical flower, not just the
same species.

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
| `?f=0..12` | Force a specific procedural species (index into the table above) |
| `?v=0..5` | Force a specific filmed clip |
| `?day=N` | Shift the day counter by N, to check the rotation without waiting |
| `?novideo=1` | Skip the clips entirely and render procedurally |
| `?t=SECONDS` | Jump to a point in the bloom timeline (negative values show the closed bud) |
| `?debug=1` | On-screen readout: species, frame time, quality tier, canvas size, GPU |
| `?q=0..6` | Force a quality tier and disable adaptive scaling |
| `?mute=1` / `?unmute=1` | Silence / re-enable notifications on this device |
| `?check=1` | Show a "notify sent ✓ / FAILED ✗" toast |
| `?still=1` | Render one frame and stop; also suppresses notifications |

## Her name

Set in Great Vibes (embedded as base64, so no network request), in three
stacked layers over a `mix-blend-mode: screen` wrapper.

The blend mode is the whole trick. Type that merely sits *on* photoreal
footage always reads as a caption; type that **adds light** reads as part of
the same photograph. Over the black it stays full strength, and where it
crosses a stem or a petal it blooms into it.

The three layers give the letters the same key light as the flower: a warm rim
offset up-left, an ivory core, and glare via `text-shadow`. The glare is
deliberately `text-shadow` and not a blurred duplicate — a blurred text block
lifts a faintly rectangular field out of the black, whereas shadows follow the
glyphs.

Two things not to "tidy up":

- **No opacity animation on `#nameWrap`.** Opacity would isolate it into its
  own group and kill the blend against the video. The reveal is a masked sweep
  instead — `mask-position` animated across an oversized feathered gradient,
  angled to the script's slant, so the letters condense out of the light.
- **Reduced motion** presents it already arrived. Getting this wrong once made
  the name invisible to anyone with Reduce Motion enabled.

An earlier version drew the name as a self-animating monoline vine, so the stem
appeared to grow into her handwriting. It read as neon wire next to photoreal
petals — a uniform-width stroke has none of the thick-thin modulation real
calligraphy does, and hand-authored beziers look crude beside a real typeface.

## Personalize

The fallback screen's name is plain text in the `.intro-name` block.
