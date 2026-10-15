# MNS Terrain Extensions — Obstacles, Water, Cliffs and Elevation

Status: design notes; deferred until after first playable delivery demo.

## Shared art grid
- Logical map cell: 96×96 px.
- Ground/grass transition autotile: 47 corner-constrained 8-neighbor variants; 32px transition band; see autotile-96-spec.md.
- Use 96×96 units for rocks, puddles, ponds, cliffs, stairs and obstacles. Larger features may occupy multiple cells.
- For assets exported in atlases, keep 1px outer margin and 2px tile separation where appropriate.

## Terrain categories
- Base terrain: ground, grass, dirt etc.
- Water: puddles and larger connected ponds/lakes, requiring edge/corner transition sets and walkability rules.
- Obstacles: rocks, boulders, vegetation; mark occupied cells as blocking or with specific traversal rules.
- Elevated land: walkable plateau surfaces and visible cliff faces.
- Stairs: 96×96 cell(s) that explicitly connect adjacent elevation levels; art and traversal metadata are separate.

## Elevation model (future)
- Each logical cell may store terrain type, elevation integer (0,1,2...), walkability and optional transition metadata.
- Neighboring cells of different elevation are NOT freely traversable; only stairs/ramps/authorized links connect levels.
- Rendering layers / y-sort are visual details, not authoritative elevation data.
- For stairs, define orientation, entry/exit, source elevation and destination elevation. Verify approach direction and collision rules.
- A cliff is a visible face between plateau heights; its drawn height need not equal one tile, and should not change the logical 96×96 ground grid.
- Use Godot TileMapLayer(s) for visual representation as appropriate, but keep traversal/elevation in a distinct gameplay model.

## Scope control
First playable demo remains flat: player movement, NPC pickup/dropoff, delivery completion. Later create a focused vertical slice with two levels, one cliff and one staircase, and test navigation and camera behavior. Do not introduce 3D or multi-floor navigation into MVP by default.
