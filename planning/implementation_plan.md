# Vampire Survivor-like Game Implementation Plan

# Goal Description
Implement a Vampire Survivor-style browser game using Phaser, React, and TypeScript.
Key features include:
- PC Browser compatibility with Cursor key movement.
- Top-down view with camera centered on the player.
- "SVG Clip" camera masking mechanism.
- Auto-firing weapon system.
- Enemy waves from all directions.
- XP drop and Level-up system (Random upgrades: Ammo, Power, Range).
- Game Architecture using Phaser for gameplay and React for UI.
- **Strict Requirement**: "SVG Clip" for camera operation (Masking).

## User Review Required
> [!IMPORTANT]
> **SVG Camera Clip**: The requirement "SVGのクリップでカメラ操作をする" is interpreted as using an SVG-based mask (or shape mask) to limit the visible game area, creating a circular or shaped viewport effect.

## Proposed Changes

### 1. Setup and Cleanup
#### [MODIFY] [src/App.jsx](file:///Users/ikomiki/workspace/phaser-rpg/src/App.jsx)
- Clean up default template code. Remove logo animations.

#### [DELETE] [src/game/scenes/](file:///Users/ikomiki/workspace/phaser-rpg/src/game/scenes/)
- Remove `MainMenu`, `Game`, `GameOver` example scenes to start fresh.

### 2. Core Architecture
#### [NEW] [src/game/scenes/BootScene.ts](file:///Users/ikomiki/workspace/phaser-rpg/src/game/scenes/BootScene.ts)
- Preload assets (use colored rectangles/circles if no assets, or placeholder SVGs).

#### [NEW] [src/game/scenes/GameScene.ts](file:///Users/ikomiki/workspace/phaser-rpg/src/game/scenes/GameScene.ts)
- Main gameplay loop.
- Initialize Systems (Player, EnemySpawner, Collision).

### 3. Feature Implementation

#### Player & Camera
- **Movement**: Vector-based velocity using Cursor Keys. 
- **Camera Follow**: `this.cameras.main.startFollow(player)`.
- **SVG Mask**: Apply a `Phaser.Display.Masks.BitmapMask` or `GeometryMask` to the main camera to achieve the "SVG Clip" effect.

#### Combat
- **Auto-Fire**: Timer event every `N` ms.
- **Targeting**: Find closest enemy `Phaser.Math.Distance.Between`.
- **Projectiles**: Physics Group for bullets. Velocity towards target.

#### Enemies
- **Spawning**: Spawn strictly outside the camera viewport (computed based on camera scroll).
- **Movement**: Move towards player coordinates constantly.

#### Progression
- **XP Orbs**: Drop on enemy destroy.
- **Pickup**: Circle collision check.
- **Level Up**:
  - Pause Phaser Scene.
  - Trigger React Modal via Event Emitter.
  - Present 3 random cards (Upgrade Ammo, Damage, Speed).
  - Resume Game on selection.

## Verification Plan

### Manual Verification
- **Movement**: Verify arrow keys move player.
- **Camera**: Verify player stays centered and SVG mask is active (vignette effect).
- **Combat**: Verify projectiles spawn and hit enemies.
- **Level Up**: Verify collecting XP opens the UI and selecting an upgrade applies stats.
