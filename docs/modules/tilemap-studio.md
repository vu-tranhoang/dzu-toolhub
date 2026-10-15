# Tilemap Studio (planned)

Create terrain templates, 47-tile bitmask transition atlases, seam previews and exports for 2D games. Separate pixel art generation from deterministic neighbor-mask selection.

Candidate first slice: import PNG, select tile size, validate source template, generate 47 corner-constrained variants where supported, paint preview, export atlas PNG + metadata. Godot TileSet export is a separate research task.

References for evaluation only: https://frameronin.com/tile , https://github.com/itsjavi/autotiler , https://github.com/Game-Development-Resources/Autotile-47 . Verify licenses/features before reuse. A flat texture alone may not supply artistic edge transitions.
