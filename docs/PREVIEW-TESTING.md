# Forever preview and animation regression checks

Run from this checkout, with the framework's CI dependencies installed:

```powershell
node tools/test/preview-layout-check.mjs "C:\path\to\RGX-Framework"
```

The harness runs the real consumer Lua and framework flow algorithm with
explicit frame seams. It checks toast/reset spacing, animation reset coverage,
unavailable nameplate coordinates, unclamped reference geometry, live/preview
task-icon sizes and anchors, level-chip rendering and selection, canonical
slider baselines, inherited General font defaults, fallback slider calls, and
that the client preview template builds its overlay through the live factory
with identical anchors. It does not emulate WoW rendering or prove
restricted-frame safety.

## Beta validation

After installing the test build and reloading the Forever beta:

- Open Animation. Toast Size and Reset All Animation Settings must be separate
  rows. Resize/reopen the panel and repeat.
- The options banner should render a real client nameplate (the same
  NamePlatePreviewTemplate mechanism the game's own nameplate settings use).
  Its style, scale, name, level display and auras must match in-world plates;
  if the template is unavailable, a Classic-constant mock is drawn instead —
  report which one you see.
- Change global and per-type animation switches/intensities and toast values.
  Reset All Animation Settings must restore `SQP.DEFAULTS`, including Kill,
  Loot and Percent main-animation switches and their displayed controls.
- On Kill, Loot and Percent, select Icon, Text and Level chip. The chip must
  appear in both the preview and live quest overlay, drawn with the client's
  level-indicator texture. General's background selection clears type
  overrides; a type reset restores General inheritance.
- With a live quest nameplate visible, compare marker and requirement-icon
  placement at default and changed General scale/X/Y/side settings. Repeat
  with non-default nameplate/UI scales.
- Change individual task sizes and offsets. Each reset/slider default must
  agree with the corresponding canonical `SQP.DEFAULTS` entry. Main overlay
  scale remains the General setting; per-type fonts inherit General unless
  explicitly overridden.
- Reload and verify persistence. Capture any Lua error with its full stack.

Keep issue #7 open until these actual-client checks pass.
