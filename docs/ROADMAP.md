# glyphspace — Roadmap

Receipt-gated, same doctrine as the constellation: no phase counts
without a sealed, replayable artifact with measured crossing rates.

## Phase 0 — Lattice + materials spec (the gate)

**Deliverable:** one grid spec shared with `glyphcast` (two repos, one
lattice — diverging specs is how constellations become debris fields).

- Cell model: coordinates, palette registry, density classes, the
  glyph→material table (albedo / transmission / emission per tone class),
  engine pin hashing.
- Gate receipt: round-trip — scene → glyph grid → raycast render →
  compare against the scene's analytic geometry (mock scene ground truth,
  free from the feed-lab).

## Phase 1 — Raycast core (`raycast`)

**Deliverable:** DDA walker over the cell lattice.

- Sightlines, shadow casting from a movable light (start with the
  feed-lab's orbital light — its ground truth is already in the receipts),
  first-person and top-down raster.
- Gate receipt: render-vs-analytic table across the mock scene frames;
  occlusions and shadow edges within one cell of truth on ≥ agreed share
  of frames, with the number published.

## Phase 2 — Zoom dynamics (`zoom`)

**Deliverable:** the mip hierarchy as a live budget system.

- Coarse grid (objects) + fine grid (texture); foveation: a gaze point
  (from an event, a query, or a tracker) moves resolution budgets around
  in real time.
- Claim to test (wager): zoom negotiation matches or beats fixed
  full-resolution rendering on downstream reader tasks at a fraction of
  the transport. Measured with the feed-lab scorer generalized to
  zoomed-reading questions.

## Phase 3 — Path tracing (`pathtrace`)

**Deliverable:** budgeted accumulation over cell materials.

- Glyphs as participating media: density classes with scattering;
  emissive glyphs (high-tone blocks) as lights.
- Compare against the analytic mock lighting where closed-form truth
  exists; labeled simulation everywhere else.

## Phase 4 — Prompt packets + robotics maps (`export`)

**Deliverable:** the two outward faces.

- Prompt packets for `pincher`: spatially grounded scene descriptions
  (regions, relations, materials, lighting) that an image model renders
  from — closing the loop the fleet canon calls "render out at the
  resolution the prompt wants."
- Occupancy/sightline maps for `glyphcam`: the low-res layer is exactly
  the map a planner wants.

## Standing rules

- One lattice spec with `glyphcast`; changes go through a pinned RFC in
  either repo, never drift.
- FAIL-first pins at every gate.
- Denominators on all claims; simulations labeled; receipts real.
