# MNS Terrain System — Pokémon-style Elevation, Cliffs, Stairs, Obstacles

Status: agreed visual/architecture direction, **implementation deferred until after first playable delivery demo**.

## Visual reference and intent
The owner supplied a Pokémon-style top-down snow map screenshot on 2026-10-15. The important features are **walkable upper plateau**, **continuous brown cliff edge with straight segments and convex/concave turns**, **walkable lower ground**, and **a staircase joining the two levels**. This is a **2D top-down / 3⁄4 ledge/elevation illusion**, not an isometric or 3D conversion. The screenshot is a design reference; do not copy copyrighted artwork into the repository.

## Common grid and atlas contract
- Authoritative logical map grid: **96 × 96 px per tile** for ground, grass, obstacles, puddles, ponds, cliff connections and stairs.
- A feature may occupy multiple logical tiles (large rock, lake, cliff run, multi-tile stair art).
- Atlas convention: **1 px outer margin**, **2 px transparent separation**, unless a specialized export explicitly documents otherwise.
- Ground↔grass autotile: **47 corner-constrained 8-neighbor variants**, with deterministic bitmask mapping and **32 px transition band**. See [autotile-96-spec.md](autotile-96-spec.md).
- Future art-authoring strategy: divide a tile into **3×3 subcells of 32×32 px** to reuse corner, edge and center art; this does not by itself change the 47-mask topology.
- Distinguish the old 2×2 terrain variation preset from true connected autotile transitions.

## Terrain and object families
| Family | Art requirements | Game rules |
| --- | --- | --- |
| Base ground / grass / dirt | Seamless center, edges and transitions | Usually walkable |
| Rocks / boulders | Individual or multi-cell sprites on 96px grid | Block occupied cells as configured |
| Puddles | Connected shallow-water shapes and banks | Walkability configurable |
| Ponds / lakes | Water centers, bank edges, inner/outer corners | Usually block or require special traversal |
| Cliff / ledge | Plateau surface + continuous side faces, corners and ends | No direct crossing between unequal levels |
| Stairs | Oriented 96px tile or multi-tile stair sequence, aligned to cliff opening | Explicit legal transition between two elevations |

## Pokémon-style elevation model
- A map cell has a **terrain type**, **integer elevation level** (0, 1, 2, …), and **walkability/obstacle flags**. This is the authoritative gameplay state; visual draw layers are not.
- The upper plateau and lower ground may reuse the same base terrain art. The cliff edge/face visually communicates the difference in height.
- Cliff art must join continuously: straight runs, turns, convex/concave corners, ends and cliff-to-stair openings. A single big mountain picture is **not** the desired solution.
- A cliff face may be drawn taller or offset beyond one tile to convey depth; its **rendered height does not change logical grid size**. The agreed 32px ground-transition band is **not** a hard cliff-height limit.
- Two adjacent cells at different elevations cannot be traversed merely because they share an edge. Stairs (and later ramps/special transitions) explicitly connect them.
- Stairs are visually tile-aligned and have **orientation**, **entry/exit cells**, **source level**, and **destination level**. Validate approach direction, collision, occupancy and movement animation.
- Draw order, Y-sorting, shadows and occlusion are presentation concerns; do not encode elevation solely by TileMapLayer order.
- Godot TileMapLayer(s) can render base terrain, cliffs, stairs and objects; a separate elevation/navigation data model decides legal movement.

## Planned validation scenario (after flat demo)
1. Build a small **Level 0** lower path and **Level 1** upper plateau.
2. Connect the plateau boundary using cliff autotile/edge pieces, including a corner and a straight segment.
3. Place one 96px-aligned staircase through an intentional cliff opening.
4. Verify player **cannot walk through the cliff**, **can ascend/descend using the staircase**, and appears at the correct level.
5. Inspect edge seams, sprite occlusion, camera follow and pathfinding. Expand to water and large obstacles afterward.

## Scope guard
First playable MNS demo remains: player movement on a flat map → NPC sender → pickup → NPC receiver → completed delivery. No elevation implementation, mountain rendering or advanced terrain generator should block that milestone.

## Related
- [MNS Autotile 96 — Ground/Grass V2](autotile-96-spec.md)
- [Tilemap Studio concept](tilemap-studio.md)
