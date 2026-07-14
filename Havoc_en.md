# Havoc Premium Suite Script Feature Documentation

Game: [Havoc](https://www.roblox.com/games/13927562399/Havoc)
En : [Havoc](Havoc.md)
---

## 1. UI Interface and Control System
* **Dear-ReGui / Orion Dual-Compatible Console**:
  * Clean, modern tabbed menu divided into six tabs: ESP, Aimbot, Silent Aim, Misc, Interface, and Settings.
  * Supports Traditional Chinese (ZH-TW) and English (EN) language switching, automatically adapting to the environment's locale.
  * Provides a configuration loading and saving mechanism (JSON format) to save and read individual user preferences.

---

## 2. Player and Bot ESP
Provides a highly customizable, performance-optimized ESP system with dual rendering engines.
* **Dual Rendering Engine Toggle**:
  * **DrowAPI Engine**: Uses Roblox's high-performance Drawing API and 3D BillboardGui for classic 3D rendering.
  * **ScreenGui Engine**: Uses an isolated gethui ScreenGui container for 2D rendering, completely bypassing Roblox CoreGui detection. Extremely light on FPS and supports hiding.
* **Three-Tier Distance Filtering and Performance Optimization**:
  1. **Under 650m (Close Range)**: Renders full ESP details including 2D bounding boxes, vertical health bars, weapon names, skeletons, and head circles.
  2. **650m - 1500m (Mid-to-Long Range)**: Only keeps name, distance, and health percentage text, removing boxes and skeletons to ensure a clean screen.
  3. **Over 1500m (Extreme Range)**: Suspends rendering entirely to prevent clutter and performance drops.
* **Simplified AI/NPC Display**:
  * Automatically hides AI names and levels, rendering only [AI] | HP: xx% [Distance] to prevent UI overlap in massive bot fights.
* **Skeleton and Head Nodes (Drawing API)**:
  * Skeletons are drawn using the high-performance Drawing API across both rendering modes.
  * Adds a small circle node for the head sitting right on top of the neck line (radius of 0.23 studs), designed to look clean without blocking your view.
* **Offscreen Indicators (Radar Triangles)**:
  * Draws offscreen triangles pointing towards enemies outside your FOV along with their distance.
  * **1200m Limit**: Non-teammate entities further than 1200 meters will not render offscreen indicators, reducing screen clutter.
  * Supports visibility-based coloring (green when visible, red when behind walls).

---

## 3. Aimbot and Silent Aim

### Aimbot
* Supports smooth aiming speed configuration (Smooth 0.1 to 1.0) to emulate natural hand movement.
* Target part locking options: Head, HumanoidRootPart, and Auto (selects the first currently visible body part).
* Independent FOV circle with wall-check (visibility check) support.
* **Auto Trigger**: While holding down the aim key (right click), the script automatically fires when the reticle aligns with the target part (within a configurable pixel error).

### Silent Aim
* Instantly redirects fired bullets to target parts without manual aiming.
* **First-Use Reminder**: If this is your first time using this script on a device (or if you have manually deleted the config file), since the RemoteFunction index has not yet been saved, you **must manually hit/kill an enemy once in-game** for the hook to capture and save the index. Every subsequent game session, raid, and script reload will load it automatically without this step.
* **SilentHitRFIndex Automatic Bootstrapping**:
  * Automatically records the child index of the randomized hit-reporting RemoteFunction inside ReplicatedStorage.Communication.Functions.
  * Re-entering games or reloading the script will instantly cache the correct function without requiring a manual hit first. It also supports automatic index correction and file saving if the ordering changes.
* Supports customizable Hit Chance (0% to 100%) and Miss Chance (0% to 100%) to emulate legit shooting.
* Wall-check support and target filtering (Players-only / Bots-only / Both).
* **One Shot Headshot**: Forces hit reporting to redirect all damage to the Head part.

---

## 4. Loot ESP and Hover Valuation
* **Advanced Loot Filtering**:
  * Minimum value threshold filter to hide cheap loot (e.g., items below 5000 cash).
  * Color-coded tags based on item value ranges (Common vs Rare/High-value loot).
* **Hover Valuation (Hover Info)**:
  * Hovering your mouse over loot crates or corpse bags will dynamically inspect its content client-side using gridStorage, displaying a list of items and total cash value next to the mouse.
* **Independent Airdrop ESP**:
  * Draws gold-colored tags showing [Airdrop Box] [Distance].
  * **Fully decoupled** from the general Loot ESP master switch. Scans recursively through workspace, Buildings, Loots, and Ignored folders to prevent missed drops.

---

## 5. Tactical Map ESP
Pressing M to open the in-game map will render the following indicators on the map frame:
* **Player and AI Pins**: Real-time position and facing direction indicator (enemies currently aiming at you turn orange).
* **Spawn Point Markers**: Map pins displaying [Spawn Point] [Distance] upon hovering.
* **Airdrop Markers**: Map pins displaying [Airdrop Box] [Distance] upon hovering.
* Includes a hover tooltip displaying HP, weapon 1, weapon 2, helmet tier, body armor tier, distance, and suspected cheater warning tags.

---

## 6. Aim Warning and Suspected Cheater Detection

### Aim Warning
* Displays a yellow text warning below the round timer whenever an enemy (within 600 studs) aims at you for longer than a threshold (default 2 seconds):
  `Warning: [Name] is aiming at you [Distance m]`.
* **AI Detection**: Supports detecting when AI bots are aiming at you.
* **Disabled for AI by Default**: Settings option AimDetectOnlyPlayers defaults to true, hiding AI warnings. Turning this option off allows AI warnings to display as `Warning: [AI] [AI Name] is aiming at you [Distance m]`.

### Suspected Cheater Detection
Automatically scans all players' leaderstats in the background. If a player exceeds the following thresholds, a **`[CHEAT]`** tag will show on their ESP, map pins, and aim warnings:
* **K/D and Player Kills**: Player kills >= 25 and K/D >= 5 (opKills >= 25 and kd >= 5).
* **Total Headshot Rate (hsRate)**: Total hits >= 30 and headshot hit rate >= 60% (hitCount >= 30 and hsRate >= 0.6).
* **Headshot-to-Kill Ratio (killHsRate)**: Total kills >= 30 and ratio >= 70% (totalKills >= 30 and killHsRate >= 0.7).

---

## 7. Misc and Exploit Bypass
* **No Recoil & No Spread**: Modifies local tool properties to remove weapon kick and bullet spread.
* **No Fall Damage**: Intercepts character fall damage RemoteEvents to negate high fall damage.
* **Force Daylight**: Overwrites in-game Lighting parameters every frame to bypass day-night cycles and provide perfect vision.
* **Landmine/Claymore ESP**:
  * Highlights nearby claymores and landmines.
