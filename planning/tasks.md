# Micro-Task Checklist

## 1. Project Cleanup
- [ ] Delete `src/game/scenes/MainMenu.js` (or ts/jsx variants)
- [ ] Delete `src/game/scenes/Game.js`
- [ ] Delete `src/game/scenes/GameOver.js`
- [ ] Remove `PhaserGame.jsx` example logic (keep component shell)
- [ ] Remove `App.jsx` example UI
- [ ] Verify `package.json` dependencies

## 2. Core Setup
- [ ] Create `src/game/scenes/BootScene.ts`
- [ ] Add `preload()` for Player sprite (placeholder)
- [ ] Add `preload()` for Enemy sprite (placeholder)
- [ ] Add `preload()` for Bullet sprite (placeholder)
- [ ] Add `preload()` for Gem (XP) sprite (placeholder)
- [ ] Create `src/game/scenes/GameScene.ts` class structure
- [ ] Register Scenes in `src/game/main.ts` (game config)
- [ ] Setup `PhaserGame` component to load new config

## 3. Player & Camera
- [ ] **Task**: Implement Player Entity
  - [ ] Add `Player` class extending `Phaser.Physics.Arcade.Sprite`
  - [ ] Initialize Player in `GameScene` at (0,0)
  - [ ] Enable World Bounds collision
- [ ] **Task**: Implement Input
  - [ ] Define `cursors` keys
  - [ ] Apply Velocity based on Input in `update()`
- [ ] **Task**: Implement Camera
  - [ ] `startFollow(player)`
  - [ ] Create Graphics object (Circle/Shape)
  - [ ] Create Mask from Graphics
  - [ ] Apply Mask to `cameras.main`

## 4. Enemy System
- [ ] **Task**: Create Enemy Class
  - [ ] Create `Enemy` class extending Sprite
  - [ ] Add `moveToPlayer` logic in `update()`
- [ ] **Task**: Enemy Spawner
  - [ ] Create timer event (1s interval)
  - [ ] Calculate random spawn position (Radius > Screen Width)
  - [ ] Spawn Enemy instance

## 5. Combat System
- [ ] **Task**: Projectiles
  - [ ] Create `Bullet` class
  - [ ] Add `fire(x, y, targetX, targetY)` method
- [ ] **Task**: Auto-Fire Mechanism
  - [ ] Add `fireTimer` to Player
  - [ ] Scan for `closest` Enemy in `enemies` group
  - [ ] If Enemy in range, Fire Bullet
- [ ] **Task**: Collisions
  - [ ] Bullet vs Enemy overlap -> `enemy.takeDamage()`
  - [ ] Enemy vs Player overlap -> `game.gameOver()`

## 6. Progression System
- [ ] **Task**: XP Drops
  - [ ] On Enemy Death -> Spawn `Gem`
  - [ ] Player vs Gem overlap -> `collectGem()`
- [ ] **Task**: Level Logic
  - [ ] Track `currentXP` and `requiredXP`
  - [ ] If `currentXP >= requiredXP`, trigger `LevelUp`
- [ ] **Task**: Upgrade UI (React)
  - [ ] Create `LevelUpModal.tsx`
  - [ ] Listen for `level-up` event from Phaser
  - [ ] Display 3 buttons (Randomly generated)
  - [ ] On Click -> Send `upgrade-selected` to Phaser -> Resume Game

## 7. Polish
- [ ] Add simple background grid/tile
- [ ] Tune speed/damage values
