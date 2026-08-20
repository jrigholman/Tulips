# Filmed blooms

Drop ten `.mp4` files in here, named exactly as below. The page picks one at
random on every visit and never repeats the one it showed last time. Any file
that is missing, slow, or unplayable falls through to the procedural flower —
so it is safe to add them one at a time.

```
tulip.mp4      parrot.mp4     peony.mp4
fringed.mp4    lily.mp4       rembrandt.mp4
```

These are tulip *varieties* — classic, parrot, double peony-flowered, fringed,
lily-flowered and Rembrandt. They look nothing like each other, so the page still
hands out a visibly different flower each visit while staying true to the gift.

To add, rename, or drop a flower, edit the `CLIPS` table in `index.html` — each
row carries the filename, the display name used in the phone buzz, an emoji for
the no-WebGL fallback, and a petal tint for the drifting petals.

## What each clip needs

| | |
|---|---|
| Aspect | **9:16 vertical**, 1080×1920 (she opens it on a phone) |
| Length | 12–20 s |
| Codec | **H.264 / AAC in .mp4**, `yuv420p`, `+faststart` |
| Size | aim under 5 MB each; she only ever downloads one |
| Content | one flower, centred, opening from bud to full bloom |
| Background | pure black, nothing else in frame |
| Camera | locked off — no shake, no pan, no zoom |
| Ending | finishes on the open flower and holds |
| **No text** | the name is drawn by the browser, not the video |

The centre of the frame must stay reasonably clear and not too bright — that is
where her name sits.

## Re-encoding to spec

If a generator hands back something heavier or the wrong size:

```bash
ffmpeg -i in.mp4 -vf "scale=1080:1920:force_original_aspect_ratio=increase,crop=1080:1920" \
  -c:v libx264 -preset slow -crf 24 -pix_fmt yuv420p -an -movflags +faststart out.mp4
```

`-an` strips audio: playback is muted anyway, since browsers only allow
autoplay without sound.
