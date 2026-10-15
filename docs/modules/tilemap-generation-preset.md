# MNS Tilemap Generation Preset — V1

## Trigger
When the owner says "tạo tilemap Grass", "tạo tilemap đất đỏ", or "tạo tilemap [terrain]", use this default unless the owner specifies otherwise.

## Pixel-exact export contract
- Canvas: **196 × 196 px** PNG.
- Layout: **2 columns × 2 rows**.
- Each tile: **96 × 96 px**.
- Outer margin: **1 px** on each edge.
- Horizontal and vertical separation: **2 px**.
- Tile origins in pixels (top-left): (1,1), (99,1), (1,99), (99,99).
- Gutters and margin: **transparent**.
- Formula per axis: 1 + 96 + 2 + 96 + 1 = 196.
- Godot 4 TileSet atlas: texture region size (96,96), margins (1,1), separation (2,2).

## Visual specification
- Crisp readable pixel art, 2D top-down / three-quarter game environment, consistent palette and lighting.
- All four cells are variants of **the requested single terrain type**, unless a transition sheet is explicitly requested.
- Distinct but compatible variation: sparse/dense details, subtle cracks/grass tufts/soil marks as relevant.
- Keep tile edges seam-friendly; avoid decorative frames or outlines that would make a visible grid.
- Avoid baked shadows that assume a different light direction between tiles.
- Do not add labels, captions, rulers, grid lines or watermarks inside tiles.
- Do not infer that four tiles constitute a complete autotile set: terrain transitions, corners, 47-tile bitmasks require separate requests.

## Generation / post-processing
Image generation alone may not honor exact dimensions or gutters. Treat the generated image as **source art**. Extract/redraw the four quadrants as needed and assemble a final **pixel-exact** transparent 196×196 PNG with 96×96 cells and exact origins. Use nearest-neighbor resizing if scaling pixel art; avoid blur. Verify actual file dimensions and alpha gutter pixels programmatically before claiming ready for Godot.

## Reusable prompt template
"Create a cohesive 2×2 pixel-art terrain tileset for **{TERRAIN}**, 2D top-down/3⁄4 rural game style, four subtly varied seam-compatible ground tiles, consistent palette, crisp pixel edges, no text, no tile outlines, no UI. Each tile will be extracted and assembled into a 96×96 pixel cell with 1px outer margin and 2px transparent separation, final atlas 196×196 px. Avoid features crossing cell boundaries unless intentionally seamless."

## Example
"Tạo tilemap Grass" → 4 compatible grass-ground variants, assembled as specified. Do not switch to winter/snow or a different biome unless requested.

## Notes
This is an asset **generation preset**, not a terrain-autotiling algorithm. For a 47-tile transition atlas, create a separate specification with its own layout and neighbor-mask rules.
