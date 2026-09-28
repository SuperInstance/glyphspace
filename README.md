# glyphspace

**Spatial reasoning over glyph grids: raycast, path-trace, and dynamic
multi-resolution zoom — where the low-res layer is geometry and the
high-res layer is texture.**

glyphspace is the spatial half of the glyph-standard constellation
(with [glyphcast](https://github.com/SuperInstance/glyphcast) for motion
and `pincher` for translation). A character grid is already a
heightfield of ink: each cell carries a density class, letterforms carry
shape, and a coarse grid and a fine grid of the same scene are a mip
hierarchy pretending to be an art project. This repo turns that into a
renderer, a mapper, and a scene representation that robots and image
models can both eat.

## The one idea

Ray tracing is trivial in the land of glyphs. Walk a ray across the cell
lattice with the oldest algorithm in games — step, read the density
class, step — and you have occlusion, shadows, and sightlines for the
price of a for-loop. Give each glyph a material table (albedo from tone
class, transmission for blanks, specular for dense blocks), swing a
light, and you are path-tracing. Zoom in: the fine grid supplies texture.
Zoom out: the coarse grid supplies objects. Foveation — the budget
negotiation the graphics industry calls variable-rate shading — falls out
of the format because every resolution of the scene already exists.

## What it produces

- **Rendered images** — a glyph-lit scene rasterized at whatever
  resolution the request wants, straight PNG, deterministic per engine
  pin.
- **Scene graphs** — the coarse grid lifted into labeled regions (the
  same reading work the feed-lab measured: orientation and discrete
  structures cross well at 0.58+; smooth gradients do not — so the
  scene graph lives at the discrete layer by design).
- **Prompt packets** — for the sibling `pincher`: a structured, spatially
  grounded description an image model can render from, without anyone
  hand-writing "cinematic lighting" into the void.
- **Maps for machines** — DDA sightlines and occupancy over glyph grids,
  for the robotics lane (`glyphcam`).

## Status — honest label

**Proposal stage.** No renderer exists here yet. What exists: the ported
chiaroscuro engine in numpy (line-faithful, feed-lab verified), measured
facts about which layers of a scene cross the format (exp001), the
temporal/zoom doctrine (exp002, exp003), and the full plan in `docs/`.

## Module map (planned)

```
glyphspace/
  glyphspace/
    lattice.py      # grid model shared with glyphcast (one spec, two repos)
    materials.py    # glyph -> (albedo, transmission, emission) table
    raycast.py      # DDA walker, sightlines, shadows
    pathtrace.py    # budgeted accumulation over cell materials
    zoom.py         # mip hierarchy, foveation budgets, zoom dynamics
    export.py       # PNG raster, scene graph JSON, prompt packet
  docs/
    ARCHITECTURE.md
    ROADMAP.md
    DEVELOPER-GUIDE.md
```

## The law this repo lives under

The freeze is the law; the crossing is always a rate. Every rendering
claim ships with its measured legibility — how much of the rendered scene
crosses to a named reader at a named resolution — or it ships labeled as
a wager.
