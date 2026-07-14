# TTK Test - ESP & Aimbot Console (v3.2) Features List

This document lists and details all core features, advanced modifications, and configuration settings in the `TTK.lua` script.

---

## 1. Visuals (ESP)
Drawing-based ESP elements rendered on screen, aligned with the server-side real `MercHitboxes`.

* **Enable ESP Master**: Toggle all ESP drawings on or off globally.
* **Show Box**: Draw a 2D bounding box around enemies.
* **Show Tracer Line**: Draw a line from the selected origin (bottom center or screen center) to the enemy's feet.
* **Show Skeleton**: Draw lines matching the player model's joints (fully aligned with R15 joints).
* **Show Player Name**: Display target player names with HP percentage (e.g., `Player [100%]`).
* **Show Distance Info**: Show the distance to the target in meters.
* **Show Player Look Line**: Draw a line pointing forward from the target's head to indicate their looking direction.
* **Green When Shootable (VisCheck)**:
  * When a target is shootable (not behind cover), the ESP color automatically changes to the visible color (default: green).
  * Excludes the player's own team character model collisions/obstacles.
  * Automatically penetrates glass objects with `Glass` or `Glass_Fragile` tags.
* **Team Filter**: Hide allies, only applying ESP to enemy players.

---

## 2. Aimbot (Camera-Simulation Aimbot)
Simulates camera movement to lock onto enemies.

* **Enable Camera Aimbot**: Toggle the aimbot logic.
* **Always On**: Lock onto the nearest target within FOV continuously, bypassing keybinds.
* **Aimbot Hotkey**: Select a hotkey (e.g. Mouse Button 2) to aim only while holding it when "Always On" is disabled.
* **Aim Target Part**:
  * `Auto` (Dynamic): Prioritize visible parts (Head -> Torso -> Leg) based on visibility checks.
  * `Head` (Fixed).
  * `Torso` (Fixed).
  * `Leg` (Fixed).
* **Smoothing**: Adjust smoothing from 1 to 20 levels. Higher levels result in slower, more human-like aiming, while 1 is instant lock.
* **Show Aimbot FOV Circle**: Render a circle representing the aimbot radius, centered on the **dynamic reticle (gun muzzle attachment position projected on screen)**.
* **Aimbot FOV Radius**: Set the aimbot pixel radius (30 - 500 px).
* **Wall Check**: Skip targets behind cover.

---

## 3. Silent Aim
Directly manipulates bullet trajectory on fire without moving the camera, ensuring shots land on target.

* **Enable Silent Aim**: Toggle silent aim.
* **Target Part**: Select target part: `Auto`, `Head`, `Torso`, `Leg`.
* **Silent FOV Type**:
  * `Center` (Fixed): Search for targets from the screen center.
  * `Dynamic` (Align Muzzle): Search for targets from the dynamic gun muzzle reticle projection.
* **Show Silent Aim FOV**: Render the silent aim radius circle.
* **Silent Aim FOV Radius**: Set the silent aim pixel radius (30 - 800 px).
* **Wall Check**: Filter out blocked targets, only aiming at exposed parts.
* **Show Target Line**: Draw a line between the silent aim detection center and the current locked target.

---

## 4. Modifications & Misc
Tweaks to weapon stats, ammo, and character mechanics.

* **Virtual Crosshair**:
  * Since hip-firing trajectories in this game deviate significantly from the screen center, this crosshair **automatically aligns to the gun muzzle attachment projection**, showing exactly where bullets will land even during recoil, gun sway, or animations.
  * Crosshair types: `Dot` (Red Dot) or `Cross` (Small Cross).
  * Configurable size and custom color.
* **No Recoil**: Hooks CameraController and resets recoil springs to zero on every frame, eliminating camera kick entirely.
* **No Spread**: Modifies runtime weapon SpreadAngle to 0, ensuring bullets travel in a straight line.
* **Disable Gun Animation**: Disables firearm viewmodel recoil and firing animations for maximum reticle stability.
* **Enable Wallbang**: Hooks BulletController and appends the map instances to the ignore list, enabling bullets to penetrate walls.
* **Force Auto Mode**: Forces all weapons to automatic fire mode.
* **Infinite Ammo**: Prevents ammo consumption and increases magazine size to 999 with 99999 reserve.

---

## 5. Throwable Modifications
* **Anti-Flashbang**:
  * Bypasses the flashbang white-out screen blur.
  * Prevents flashbang ear-ringing sound effects.
  * Removes the sprint blocking state caused by flashbangs.

---

## 6. Settings
* **Language**: Switch interface language between **Traditional Chinese (zh-tw)** and **English (en-us)** with immediate UI reloading.
* **Auto-detect Language**: Detects language preference at startup by reading `Tsetingnil_script/keysystem.json`.
* **Max Render Distance**: Limit ESP visual rendering distance (100m - 5000m).
* **Line Thickness**: Pixel thickness for drawings.
* **Opacity**: Opacity value for text and drawings.
* **Tracer Origin**: Set Tracer Line origin position to Bottom Center or Screen Center.
* **Colors**:
  * Enemy Color
  * Ally Color
  * Visible (VisCheck) Color
* **Configuration**:
  * **Save Config**: Save current settings to `Tsetingnil_script/TTK/config.json`.
  * **Load Config**: Manually reload the saved configuration.
  * **Auto Load Config**: Automatically load saved settings upon script startup.
* **Unload ESP**: Restore all hooks, clean up drawing objects, close GUI, and free up memory.
