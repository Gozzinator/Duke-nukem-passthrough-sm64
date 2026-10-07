# Duke-nukem-passthrough-sm64
A mod that allows passthrough of duke 3d eduke32 version to have first person and weapons and in the future much more...


# Duke Nukem x Super Mario 64 Passthrough Overlay (Phase 1)

Shows Duke Nukem 3D's weapon view (running in EDuke32) on top of Super Mario 64
(running in sm64coopdx). A small Python program captures the EDuke32 window,
makes one colour transparent, and draws the rest in a click-through,
always-on-top overlay. Windows 10/11 only.

This is Phase 1 (visuals only). Input forwarding and weapon damage come later.

## What you need

- Windows 10 or 11
- Python 3.10+ (python.org, tick "Add python.exe to PATH") - only for building/running from source
- EDuke32 (eduke32.com) plus your own copy of Duke Nukem 3D's `DUKE3D.GRP`
- sm64coopdx (GitHub releases) plus your own legally dumped SM64 ROM

No game files are included in this zip.

## Build the program

1. Unzip this folder anywhere.
2. Double-click `build.bat`.
3. When it finishes, your program is at `dist\duke_overlay.exe`.

To skip building and run from source instead, double-click `run.bat`.

## Use it

1. Start EDuke32 in a window (not fullscreen, not minimised).
2. Start sm64coopdx in borderless windowed (or windowed) mode.
3. Run `dist\duke_overlay.exe` (or `run.bat`).
4. Anything EDuke32 shows now appears over SM64, with the key colour transparent.
5. Quit by closing the console window or pressing Ctrl+C in it.

## Making only the gun show

You want EDuke32 to display the weapon but not Duke's world.

1. Open Mapster32 (ships with EDuke32) and make a tiny sealed room.
2. Paint floor, ceiling and walls with a solid-colour tile.
3. Either paint it magenta (default key colour), or paint it pure black and set
   `KEY_COLOR = (0, 0, 0)` in `duke_overlay.py`, then rebuild.
4. In EDuke32, shrink the view with the screen-size keys to hide the status bar.

Black is easiest, but any pure-black pixels in the gun art turn transparent too.
If that looks bad, use magenta.

## Settings

Edit the top of `duke_overlay.py`, then run `build.bat` again:

| Setting        | Meaning                                                        |
|----------------|----------------------------------------------------------------|
| `WINDOW_NAME`  | Part of the EDuke32 window title. Must match.                  |
| `KEY_COLOR`    | RGB colour made transparent.                                   |
| `CROP`         | Pixels trimmed (left, top, right, bottom) to hide title bar.   |
| `OVERLAY_POS`  | Top-left of overlay on screen.                                 |
| `OVERLAY_SIZE` | (width, height), or None for the full primary screen.          |
| `FPS`          | Overlay refresh rate.                                          |

A typical crop for a standard window frame is `CROP = (8, 31, 8, 8)`.

## Troubleshooting

- **Nothing appears:** check `WINDOW_NAME` matches the EDuke32 title, and that
  EDuke32 is not minimised.
- **Overlay is black or magenta everywhere:** EDuke32 is showing the key colour
  across the whole view. Make sure the weapon is visible in the map, and check CROP.
- **Pink or black fringes around the gun:** the key colour must match exactly.
  Don't enable filtering or anti-aliasing in EDuke32 for the room surfaces.
- **SM64 hides the overlay:** use borderless windowed mode, not exclusive fullscreen.
- **Build errors:** make sure Python is on PATH, then rerun `build.bat`.
  If `windows-capture` fails to install, update Python to 3.10 or newer.
- **Antivirus flags the exe:** PyInstaller exes sometimes trigger false positives.
  Run from source with `run.bat` instead.

## Roadmap

- Phase 2: forward fire and weapon-switch keys to EDuke32 while SM64 keeps focus
- Phase 3: sm64coopdx Lua mod that damages enemies in front of Mario
- Phase 4: first-person camera, ammo sync, sound

## Legal

Duke Nukem 3D and Super Mario 64 are the property of their respective owners.
This tool contains no game code or assets. Use your own legally obtained copies,
and do not redistribute game files with it.