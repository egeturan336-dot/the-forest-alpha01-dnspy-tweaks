# the-forest-alpha01-dnspy-tweaks
# The Forest (Alpha 0.01) — dnSpy Sandbox & Movement Tweaks

C# method modifications and notes for **The Forest Alpha 0.01** (Unity Mono / .NET 3.5) inspected and edited via **dnSpy**.

> **Note:** Original game binaries and `Assembly-CSharp.dll` are not included in this repository. Only modified code snippets and setup notes are shared.

## What Was Added / Changed

### 1. Buildhack / Non-Consuming Materials (`Craft_Structure`)
* Removed player material consumption calls (`UsedWood`, `UsedStick`, `UsedLeaf`, `UsedRock`, `UsedHead`, `UsedLeg`, `UsedArm`) inside `Add*` methods so building materials are not deducted from the player.
* Added bounds and null checks on `*Render` arrays to avoid index/null errors during placement.
* Sent `DropLog2` and `DropLog1` messages inside `Build()` so any held logs can be dropped cleanly once construction finishes.

### 2. Infinite Log Stock While Keeping Drop Support (`PlayerItems`)
* Removed `PlayerItems.Logs--` in `UsedWood()` so log count does not decrease when placing logs onto structures, while still hiding/clearing held log visuals properly.
* Preserved log-dropping behavior (`DropLog1` / `DropLog2`).

### 3. Speedyrun / High Movement Speed & Stamina (`FirstPersonCharacter`)
* Increased movement speed and acceleration limits inside `FixedUpdate()` (`runSpeed`, `walkSpeed`, and `maxVelocityChange`) for faster traversal.
* Kept stamina topped up during running so sprint speed is not interrupted.

## How to Apply with dnSpy
1. Back up `Assembly-CSharp.dll` before making any edits.
2. Open `Assembly-CSharp.dll` in **dnSpy**.
3. Locate the target class and method, right-click -> **Edit Method (C#)**, apply the changes, and click **Compile**.
4. Go to **File > Save Module...** to save the modified DLL.
