# Red-Dead-Redemption-Stereoscopic-3DMod
Red Dead Redemption-Stereoscopic-3DMod Patch

## Stereo 3D (`[Stereo3D]`)

The mod can also add real geometric stereo 3D, layered on top of (or fully
independent from) head tracking — same method as the companion document
*Making 6DOF Mods 3D — A General Method*. Because this mod already drives the
camera by position + orientation (RedHook natives), separation is just
another vector added in the cave; convergence is a Present-time image shift
applied by a small DirectX 12 compositor the mod installs alongside the
camera hook.

- **`Enabled=0` by default** — this is DX12-only (RDR's 2024 port has no DX11
  path) and hooks `IDXGISwapChain::Present` / `ID3D12CommandQueue::ExecuteCommandLists`
  by vtable, so treat it as more experimental than the tracking layer. Set
  `[Stereo3D] Enabled=1` to turn it on.
- **`OutputMode`** picks the packing: `1` SBS (default, works with 3D TVs set
  to Side-by-Side-Half, SBS players, and desktop VR viewers), `2` TAB, `3`
  Line, `4` Column, `5` Checkerboard. `6` (VR full-resolution shared surface)
  is **not implemented** in this build — it falls back to SBS.
- **`SeparationMM`** is 3D strength as a real IPD in millimetres (55–75 is the
  realistic human range; no upper limit). **`ConvergenceDistance`** is where
  the scene sits on the screen (world units — RDR1 reads roughly 1 unit = 1
  metre, matching the lean units above).
- It renders each eye on **alternating frames** (AFR) rather than doubling
  render cost, so each eye updates at half your frame rate. This costs a
  touch of motion softness during fast camera motion — raising/steadying your
  frame rate is the single biggest lever if that bothers you.
- **Cadence log:** with `[General] Diagnostics=1`, `HeadTracking.log` prints a
  `[3D][cadence]` line once a second (`present/s`, `camWrite/s`, `eyeflips/s`,
  `held/s`). On a healthy run `eyeflips/s` tracks `present/s` closely and
  `held/s` stays low — check this on first launch.


## Install

1. Install **RedHook** (ScriptHook for RDR1) into your game folder — the folder
   that contains `RDR.exe`. RedHook:https://www.nexusmods.com/reddeadredemption/mods/192
2. Copy **`RDR-HeadTracking.red`** and **`HeadTracking.ini`** into that same
   folder (next to `RDR.exe`).
3. Launch the game.

4. If the crash Edit the RedHook.ini [DirectXHook]
; Set this to true if you are experiencing crashes or other issues (WARNING: This will completely disable ingame console UI and some other rendering features)
Disabled=true

## Settings

-Enable VSYNC 
-Disable Motion Blur
-Disable DLSS
