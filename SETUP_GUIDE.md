# 3D Architecture Simulator - Setup Guide

## Project Structure Created

```
Assets/
├── Scripts/
│   ├── Building/
│   │   ├── BuildableObject.cs      # Base class for all buildable objects
│   │   ├── Wall.cs                 # Wall with start/end points
│   │   ├── Floor.cs                # Floor with size/position
│   │   ├── Door.cs                 # Interactive door (E to open/close)
│   │   └── Window.cs               # Window object
│   ├── Editor/
│   │   ├── GridManager.cs          # 2D grid with snap-to-grid
│   │   ├── SelectionManager.cs     # Object selection/deselection
│   │   └── BuildModeManager.cs     # Tool handling (wall, floor, door, window, furniture)
│   ├── Player/
│   │   └── PlayerController.cs     # First-person WASD + mouse look
│   ├── UI/
│   │   ├── UIManager.cs            # All UI panels and interactions
│   │   └── UICreator.cs            # Auto-creates UI at runtime
│   ├── SaveSystem/
│   │   └── SaveManager.cs          # Save/load projects as JSON
│   ├── Furniture/
│   │   └── FurnitureItem.cs        # Bed, Sofa, Table, Chair
│   ├── GameManager.cs              # Main game state controller
│   └── SceneSetup.cs               # Auto-setup scene on start
├── Prefabs/ (empty - created at runtime)
├── Materials/ (empty)
└── Scenes/ (empty)
```

## How to Set Up in Unity

### 1. Create New Unity Project
- Open Unity Hub
- Create new 3D (URP) project
- Name it "ArchitectureSimulator"

### 2. Import Scripts
- Copy the `Assets` folder into your Unity project
- Or create the folder structure manually and copy the `.cs` files

### 3. Create Main Scene
1. File → New Scene
2. Save as `Assets/Scenes/MainScene.unity`
3. Add to Build Settings (File → Build Settings → Add Open Scenes)

### 4. Setup Scene (Automatic)
1. Create empty GameObject named "GameController"
2. Add component `SceneSetup`
3. Add component `UICreator`
4. Press Play - everything sets up automatically!

### 5. Manual Setup (Alternative)
If you prefer manual setup:

**GameController Object:**
- Add `GameManager`
- Add `GridManager`
- Add `BuildModeManager`
- Add `SelectionManager`
- Add `SaveManager`

**Player Object:**
- Create empty "Player"
- Add `PlayerController`
- Add `CharacterController` (auto-added)
- Tag as "Player"

**Main Camera:**
- Position: (0, 15, 15)
- Rotation: (45, 0, 0)

## How to Use

### Build Mode (Default)
1. **Select Tool** - Click objects to select/move/delete
2. **Wall Tool** - Click to set start point, drag, click to set end point
3. **Floor Tool** - Click anywhere to place 4x4 floor
4. **Door Tool** - Click to place door (1m wide, 2.1m tall)
5. **Window Tool** - Click to place window (1.5m wide, 1.2m tall)
6. **Furniture Tool** - Select type from dropdown, click to place

### Color Picker
- Select any object → Color Picker panel appears
- Use RGB sliders or type HEX value
- Click Apply to change object color

### Walk Mode
- Click "ENTER HOUSE" button
- WASD to move, Mouse to look, Shift to run
- E to open/close doors (when near)
- Collision prevents walking through walls
- Click "EXIT TO BUILD MODE" to return

### Save/Load
- F5 = Save project
- F9 = Load last project
- Files saved to `Application.persistentDataPath/Projects/`

## Controls Summary

| Mode | Key | Action |
|------|-----|--------|
| Build | Left Click | Place/Select object |
| Build | Right Click | Cancel wall / Deselect |
| Build | Delete | Delete selected |
| Build | Escape | Deselect / Return to Select tool |
| Walk | WASD | Move |
| Walk | Mouse | Look around |
| Walk | Shift | Run |
| Walk | E | Open/Close door |
| Walk | ESC | Exit to Build Mode |
| Both | F5 | Save |
| Both | F9 | Load |

## Next Steps for Enhancement

1. **Better Furniture** - Replace cubes with actual models
2. **Wall Snapping** - Snap walls to other walls/grid intersections
3. **Room Detection** - Auto-detect enclosed rooms
4. **Multi-floor** - Add floor switching
5. **Roof Tool** - Auto-generate roof
6. **Better UI** - Tool icons, tooltips, property panels
7. **Undo/Redo** - History system
8. **Texture Support** - Material browser

## Troubleshooting

**UI not showing?**
- Check Canvas Scaler is set to "Scale with Screen Size"
- Ensure EventSystem exists in scene

**Player falls through floor?**
- Check GroundLayer in PlayerController includes "Default"
- Ensure floor has collider

**Walls don't snap?**
- Check GridManager exists and GridSize = 1

**Can't select objects?**
- Check SelectionManager exists
- Ensure objects have BuildableObject component
- Check raycast hits colliders (not triggers)