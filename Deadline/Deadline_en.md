# Deadline Premium Suite Game Script Feature Documentation

Game: [Deadline](https://www.roblox.com/games/12144402492/Deadline-Lobby)
Zh : [Deadline](Deadline.md)
---

## 1. UI Interface & Control System
* **Dear-ReGui Console Panel**:
  * Features 5 main functional tabs: Visuals, Aimbot, Silent Aim, Misc, and Settings.
  * Supports real-time language switching between English (EN) and Traditional Chinese (ZH-TW), and dynamically adapts the default language based on the keysystem.json configuration file.
  * Provides a complete local configuration system (JSON) to auto-save, hand-save, and load player preference settings.

---

## 2. Visuals ESP System
Offers a highly customizable, high-performance ESP system with dual rendering engines.
* **Dual Rendering Engine Switch**:
  * **ScreenGui Engine**: Uses an emulated ScreenGui container to render ESP, bypassing traditional CoreGui detection, placing minimal load on FPS.
  * **Drawing Engine**: Uses Roblox's native Drawing API for smoother and cleaner rendering of lines.
* **Rich Entity ESP Options**:
  * **Box ESP**: Supports Corner and Full box styles, with optional semi-transparent color filling.
  * **Skeleton ESP**: Renders bone structures and draws a small circle node for the head.
  * **Other Visual Details**: Display names, distance, equipped weapon name, and Night Vision Goggle (NVG) tags.
  * **Tracer Lines & Origins**: Supports tracer lines pointing to targets, with customizable origins (Top Center, Screen Center, or Bottom Center).
  * **Moving Indicator**: Visualizes the movement state and velocity direction of targets.
* **Filtering & Tactical Analysis**:
  * **Visibility Check (VisCheck)**：When targets are visible (unblocked), boxes and bones dynamically transition to a customizable color (default is green).
  * **Team Filter**: Automatically hides allies to prevent UI clutter during intense team fights.
  * **Off-screen Arrows**: Displays directional triangular arrows with distance at screen edges when enemies are outside the camera field of view, preventing backstabs.
  * **Aiming Warning**: Displays a prominent warning on the screen center when an enemy aligns their crosshair onto you.
* **Grenade ESP & Warning**:
  * **Grenade ESP**: Renders real-time markers for active throwables (grenades, etc.).
  * **Landing Zone & Blast Ring**: Estimates the projectile landing zone and draws a dangerous blast ring, with customizable warning distance and blast radius.
* **2D Radar & HUD**:
  * **Mini Map Radar**: Renders a 2D radar on the top-right corner of the screen to track relative enemy directions.
  * **Radar HUD**: Draws radar indicator lines on the bottom area of the screen to assist with tactical positioning.
* **World ESP**:
  * **Ammo/Supply Box ESP**: Tracks supply crates and ammo lockers with customizable display colors.

---

## 3. Aimbot & Bullet Drop Compensation
* **Camera Aimbot**:
  * Supports customized hotkey bindings to activate or toggle aimbot.
  * **Aim Part Selection**: Supports Auto (Smart body part selection based on visibility), Head, Neck, Torso, and extremities (shoulders, elbows, knees).
  * **Smoothing Control**: Customizable smoothing factor. Setting to 1 yields direct lock, while higher values provide smooth transitions to mimic natural mouse tracking.
* **Aimbot FOV & Obstacle Filters**:
  * Features an independent FOV circle that can follow the mouse cursor or be hidden.
  * **Wall Check**: Automatically ignores hidden targets behind obstacles or walls.
* **Bullet Drop Compensation**:
  * Dynamically calculates physical bullet gravity drop and muzzle velocity for Deadline's unique ballistic system, adjusting the aim angle to ensure precise long-range hits.

---

## 4. Silent Aim & Ballistic Redirection
* **Silent Aim**:
  * Redirects projectile flight paths directly to the target without needing to align the camera crosshair onto them.
  * **Aim Part Selection**: Supports Auto (unblocked part priority), Head, Neck, Torso, etc.
* **Silent Aim FOV & Rules**:
  * Features an independent Silent Aim FOV circle to restrict active angles.
  * Supports Wall Check to filter out unreachable targets behind walls.
  * Supports limiting the maximum silent aim range.
  * Supports drawing target lines to clearly display which target is currently locked.
* **Exploit Bypass**:
  * Hooks the low-level functions `NetworkEncode.write_exact_position`, `caster.fire`, and `caster.network_hit` to alter bullet unit vectors and rewrite hit part names in network packets, preserving performance and cleanly bypassing game anticheat detections.

---

## 5. Misc & Combat QoL Modifications
* **Character & Weapon Modifiers**:
  * **No Recoil**: Completely eliminates screen shake and muzzle kickback when firing.
  * **No Spread**: Eliminates random bullet dispersion, forcing all bullets to land precisely at a single point.
  * **Infinite Stamina**: Infinite running endurance.
  * **Infinite Scope Stamina**: Infinite holding breath duration when aiming with scoped optics.
  * **Disable Suppression**: Completely blocks screen blurring, shaking, and visual distortion caused by enemy bullet suppression.
  * **Swift Weapon Switch**: Eliminates or shortens switch-weapon animation delays.
  * **Remove Weight**: Removes running speed penalties from carrying heavy weapons and attachments, boosting mobility when combined with ergonomics multipliers.
  * **Dynamic Scope**: Optimizes and improves the activation and rendering behavior of high-magnification scopes.
  * **Force Daylight**: Locks local time to afternoon and removes fog, bypassing map night cycles or heavy mist for perfect visibility.
  * **Remove Grenade Effects**: Immune to flashbang blinding effects and stops rendering smoke grenade particle clouds.
* **RPG Modification**:
  * **Enlarge Blast Radius**: Modifies explosion parameters to significantly expand the RPG rocket blast damage radius.
* **Combat QoL**:
  * **Exact Ammo**: Displays exact remaining magazine bullet count on the HUD permanently without checking.
  * **No Lens Flare**: Removes visual glare from direct sunlight or bright lamps.
  * **No Stamina Shake**: Removes physiological scope swaying caused by low stamina or fast movement.
  * **Interaction Reach**: Extends the pickup and interaction range for supply boxes, vehicles, and objects.
* **Performance Optimization**:
  * **Disable Muzzle Flash**: Removes fire muzzle flash particle effects to avoid blocking vision.
  * **Disable Bullet Tracers**: Removes bullet tracer lines, improving rendering performance and allowing stealthy shooting.

---

## 6. Detailed Customizations (Settings)
* **Max Render Distance**: Adjusts the furthest range for ESP rendering to save client resources.
* **Visual Adjustments**: Customizes line thickness, opacity, chams transparency, and box fill opacity.
* **Fonts & Colors Customization**:
  * Adjusts ESP text size and font style (UI, System, Plex, Monospace).
  * Customizes different colors for enemies, allies, and visible targets.
