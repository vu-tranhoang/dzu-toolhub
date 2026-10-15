# MNS Autotile 96 — Ground/Grass V2

Status: design decision / future implementation. Supersedes the four-independent-variations interpretation for terrain transitions; does not delete the separate 2x2 preset for decorative variations.

## Agreed now
- Main logical tile: **96 × 96 px**.
- Transition border band: **32 px** (one third of a tile).
- Ground ↔ grass transitions must connect across adjacent tiles, including straight edges, outer corners and inner corners.
- Use a **47-variant corner-constrained 8-neighbor autotile** as initial target; each atlas entry must correspond to a deterministic neighbor mask. No random set of 47 images.
- Atlas margin: **1 px**, separation: **2 px** (Godot atlas texture settings).
- Proposed layout: **8 columns × 6 rows** (48 slots, 47 used).
- Pixel-exact canvas: **8×96 + 7×2 + 2×1 = 784 px** wide; **6×96 + 5×2 + 2×1 = 588 px** high.
- Required test cases: continuous grass area, isolated dirt/grass islands, straight paths, L-shapes, concave and convex corners, and seam inspection.

## Later
- Subdivide each 96×96 tile into a **3×3 grid of 32×32 subcells**.
- This enables reusable center, edge and corner artwork and additional tile variants/terrain styles.
- Subdivision alone does not imply more autotile neighbor masks; define expanded rules separately.

## Implementation caution
- A 47-tile atlas is not valid just because it contains 47 visually different squares. Require mapping between each image and its neighbor bitmask and validate edge/corner compatibility.
- Distinguish terrain type from overlay/transition; do not create permanent hard-coded borders that cause seams.
- The current 2×2 terrain variation preset remains a different task. When user requests **autotile**, use this spec, not the 2×2 preset.
