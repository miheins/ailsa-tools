# Ailsa Image Tools

Two browser tools for producing Ailsa brand imagery. Everything runs locally in the browser: no server, no build step to use it, no uploads leave your machine.

Open `index.html` directly, or serve the repo with GitHub Pages.

## Image texture

Turns a landscape photo into a brand texture.

1. **Image & sky mask:** upload, drop or paste an image (Ctrl/⌘+V). The sky is detected from the top edge and removed. Controls: tolerance, smoothing, edge shift, feather, sky limit, sky seen through gaps, and picking sky points by hand. The Mask preview shows the removed area in red.
2. **Adjust image:** brightness, contrast and saturation. These apply to the photo only, not the background or overlays.
3. **Dot grid:** spacing, dot size, colour, opacity, and above or below the tints.
4. **Tints 1 and 2:** colour, opacity and blend mode (colour dodge, luminosity, saturation, screen).
5. **Export:** PNG (transparent sky when Background is off) or JPG, at the image's full resolution.

**Auto look** reads the land (ignoring the sky) and sets brightness, contrast, saturation, a background tint, the dot grid and one tint. **Undo** restores your previous settings.

Every colour control has swatches from the Ailsa light palette: Lime, Blue and Red 100 to 300, White, and Olive 0 to 300.

## Orbit

Image cards orbit the Ailsa mark, scaling up at the front and down at the back to fake depth, with spokes to the centre.

- Image slots: add, replace, remove, drag and drop. You can also set a custom centre image.
- Orbit width, depth tilt, roll, speed, scatter, front and back scale, back fade, card size and shape, spokes and stage size.
- Play/pause button (Space works too), direction, angle scrubber, and drag to rotate.
- Export a PNG frame, a video loop of one revolution (WebM, or MP4 in Safari), or **embed code**: a self-contained `<div>` and script for any web page. The embed pauses when off-screen and respects reduced-motion settings.

## Repository layout

| Path | What it is |
| --- | --- |
| `index.html` | The built page with both tools. This is the file to open or host. |
| `src/texture.html` | Image texture source. Also works as a standalone page. |
| `src/orbit.html` | Orbit source. Also works as a standalone page. |
| `build.py` | Combines the two sources into `index.html`. |

Edit the files in `src/`, then rebuild:

```sh
python3 build.py
```

The build namespaces each tool's element ids (`t-`, `o-`) and CSS so the two can share one page. In tool scripts, look up elements with `$('id')`, never `document.getElementById`.

## Known limits

- **No loading from a URL.** Browsers block reading pixels from images on other sites unless those sites allow it, and most image hosts don't. Copy the image in your browser and paste it instead.
- **The sky mask works on colour and edges.** It doesn't recognise what a sky is. Clouds count as land at low tolerance. Hazy or low-contrast horizons can leak, so use Sky limit for those.
- **Video export records in real time** (one revolution) and depends on the browser's MediaRecorder support.
- **Default images are embedded** in the sources as base64. Check you have the rights to any image before publishing it.
