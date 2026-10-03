# WallCue 0.1.8

[简体中文](README-CN.md) | **English**

**Test build for Beat Saber PC 1.44.1**

WallCue adds visual wall warnings and collision feedback to Beat Saber. It is designed for FitBeat and other maps with frequent crouching and dodging. Wall outline cues, a wall-hit counter, and a fixed-position hit icon make it easier to tell whether you cleared a wall—especially a thin wall that passes too quickly to notice.

This is a **PC mod**. It can be used when playing the PC version through a Quest headset via PC streaming. It does **not** support standalone Quest Beat Saber.

Mod for Beat Saber PC 1.40.8 also [available here](https://github.com/Hikari31768/WallCue/releases)

## Features

<img width="544" height="419" alt="WallCue_graphical_sample" src="https://github.com/user-attachments/assets/d507e55f-17fd-412b-92a1-6eb10471c99f" />

### Wall outline cues

- **Yellow:** Staying at your current head position would put you in the path of an approaching wall, or you are within the configured safety margin of its edge.
- **Flashing red/transparent:** The game is detecting a head collision with the wall.
- **Original appearance:** You are clear of the warning area or have moved out of the wall.

Yellow cues update as you crouch or move sideways. They use your current head position; they do not predict your next movement. A yellow cue does not mean a collision has already occurred.

### Wall Hits counter

A two-line HUD counter displays `Wall Hits` above the number of walls hit in the current run. Each newly hit wall adds 1, and the number turns red for **0.5 seconds** before returning to white.

Each wall is counted only once. Staying inside a wall, or leaving and re-entering the same wall, does not add another hit. Different walls are counted separately. The count resets when starting or restarting a map.

### Wall Hit Icon

Each new wall hit triggers a white icon at a fixed HUD position:

**0.1-second fade-in → 0.3-second hold → 0.1-second fade-out**

The icon completes its animation even if the wall has already passed. Hitting several walls in quick succession refreshes the display instead of stacking multiple icons.

The counter and icon use the game's actual **head-collision** results. Saber contact with a wall does not count. WallCue does not change collision detection, health, or scoring rules.

## Installation and updates

Install versions of the following dependencies that are compatible with **Beat Saber 1.44.1**:

| Dependency | Required version |
| --- | --- |
| BSIPA | 4.3.6 or later within 4.x |
| SiraUtil | 3.3.1 or later within 3.x |
| BeatSaberMarkupLanguage (BSML) | 1.14.1 or later within 1.x |
| Counters+ | 2.3.12 or later within 2.x; tested with 2.3.12 |

Dependencies must support your game version as well as meet these version requirements. They are not included in the WallCue package.

1. Close Beat Saber.
2. Copy `Plugins/WallCue.dll` from the release archive into your game's `Plugins` folder.
3. When updating, replace the existing DLL. Do not keep renamed copies of older versions alongside it.
4. Launch the game and configure the mod using the settings below.

If you use BSManager, install the DLL into the **1.44.1 instance** you intend to play. The icon is embedded in the DLL; no separate image file is needed. HitScoreVisualizer and Enhancements are not required.

You can keep your existing configuration when updating. To uninstall, close the game and remove `Plugins/WallCue.dll`.

## Warning distance and sensitivity

Open **Mods → WallCue** on the left side of the song-selection screen.

<img width="848" height="625" alt="MetaScreenshot1791016929" src="https://github.com/user-attachments/assets/2f7c78c8-4cdf-406f-9417-2773b640327f" />

| Setting | Function | Default |
| --- | --- | --- |
| Limit warning distance | When enabled, limits how far ahead yellow warnings appear. When disabled, there is no distance limit. | Off |
| Warning distance | Sets the forward warning distance from 5 to 25 metres, in 0.1-metre increments. | 10.0 m |
| Sensitivity | Adds a safety margin to yellow cues, from 0 to 10 centimetres in 1-centimetre increments. | 5 cm |

When the distance limit is off, the distance slider is disabled but retains its previous value. Enable the limit to adjust it by dragging the slider or using the buttons at either end.

**Higher sensitivity means more clearance is required before the yellow cue disappears.** For example, increasing the margin from 5 cm to 10 cm means you need to crouch lower or move farther sideways to clear the warning. At 0 cm, there is no extra margin, but walls directly in your path still trigger warnings. Sensitivity does not change the game's actual collision detection.

The distance limit only affects yellow warnings for approaching walls. It does not restrict red collision flashing, the counter, or the hit icon. Unlimited distance still applies only to walls that the game has already spawned; it does not reveal every wall in the map in advance.

Changes are saved automatically. Adjust the settings and start a map—no game restart is needed. Settings are shared across maps; there are no automatic per-map presets.

If the WallCue tab is missing, use the arrow buttons to browse the Mods tabs, or check the eye button to see whether the tab is hidden.

## Counter and icon settings

Open **Counters+ settings → Counters**.

<img width="950" height="635" alt="MetaScreenshot1791016169" src="https://github.com/user-attachments/assets/a33b2a4f-83aa-4cfc-8b3f-27da0b643333" />
<img width="955" height="616" alt="MetaScreenshot1791016187" src="https://github.com/user-attachments/assets/53d72d3d-e673-4ce9-96a9-25e9e6f84175" />

| Item | Purpose | Default placement |
| --- | --- | --- |
| Wall Hits | Wall-hit counter | Below Combo, Distance 2 |
| Wall Hit Icon | Fixed-position collision icon | Over Highway, Distance 0 |

Both items are enabled by default. Each has its own **Enabled**, **Position**, **Distance**, and **Canvas** settings. Use Counters+ Canvas settings for finer control over placement and overall scale.

The `Distance` setting here controls **HUD placement**. It is separate from WallCue's warning distance.

The Counters+ preview may show the text `Wall Hit Icon` as a placeholder. The actual icon appears during gameplay when a collision occurs.

The wall outline controls are also available under **Counters+ → Wall Hits**, in its additional settings:

| Setting | Function |
| --- | --- |
| Wall frame cues | Enables yellow outline cues and red collision flashing. Does not disable the counter or icon. |
| Test: all walls yellow | Diagnostic outline test. Leave this off during normal play. |

To use only the counter and icon, turn off `Wall frame cues`.

## Compatibility

| Map type or mode | Current status |
| --- | --- |
| Standard maps / FitBeat | Outline cues, counter, icon, and settings have been tested in-game. |
| Mapping Extensions (ME) maps | Tested successfully on a map using ME. More testing of unusual walls is welcome. |
| Noodle Extensions (NE) maps | **Outline effects are automatically disabled; the counter and icon remain active.** Tested in-game with 0.1.8. |
| BSPlus multiplayer | Tested successfully in the tester's setup. |
| Other multiplayer implementations, Campaign, tutorials, replays, and other game versions | Not sufficiently tested. |

On NE maps, decorative or non-collidable walls do not count as hits merely because they visually pass through your head. Feedback is triggered only by collisions detected by the game. Disabling outline effects on NE maps is intentional; they are restored when returning to a standard map. Automatic NE detection relies on the selected difficulty declaring Noodle Extensions.

If another mod hides wall outlines, WallCue does not force them to become visible. The counter and icon can still work independently. Compatibility with animated wall colours, unusual animations, and different combinations of mods needs further testing.

## Troubleshooting

### The counter or icon is missing

Check the Counters+ master switch, the item's `Enabled` setting, its position and Canvas, and any settings that hide the HUD. The icon is normally hidden and appears only when you hit a wall.

### Walls do not turn yellow

Make sure `Wall frame cues` is enabled. Check the warning distance and whether your head is already in a safe position. NE maps intentionally have no outline cues. Other mods that hide wall outlines may also affect visibility.

### Every wall stays yellow

Turn off `Test: all walls yellow`.

### Red flashing is hard to see on thin walls

Outline flashing lasts only while an actual collision is occurring, so it can be very brief on thin walls. Use the counter's red flash and the hit icon for feedback that lasts 0.5 seconds independently of the wall.

### The counter displays `--`

Collision tracking is unavailable for the current level. This does not mean zero hits. Please include a log when reporting the issue.

## Development and feedback

WallCue is under active development. Bug reports, compatibility reports, and pull requests are welcome.

### Build requirements

- Python 3
- .NET SDK 8 or later
- Beat Saber PC 1.44.1
- BSIPA, SiraUtil, BSML, and Counters+ installed

Run the following from the repository root:

```powershell
python build.py --game "D:\Path\To\Beat Saber"
```

### Reporting an issue

Please include:

- Beat Saber and WallCue versions.
- Relevant mods and their versions.
- The map link or BeatSaver ID and selected difficulty, including whether it uses NE or ME and whether you were playing multiplayer.
- Steps to reproduce the issue, relevant settings, and expected versus actual behaviour.
- The latest `_latest.log` from the game's `Logs` folder for the affected session.
- Screenshots or a recording where helpful. For visual issues, a headset recording is especially useful.

## AI-assisted development

WallCue is developed with extensive use of AI-assisted programming tools.

The project owner defines the requirements, intended behaviour, compatibility goals, and release decisions, and performs iterative in-game testing on real Beat Saber setups. AI tools are used extensively for code implementation, debugging, log analysis, refactoring, and documentation.

AI-generated changes are validated through builds and practical testing before release, but the source code should not be assumed to have received a complete line-by-line manual audit.

Human contributions submitted through GitHub issues and pull requests are reviewed and tracked through the repository history.

## Author

SD無 (GitHub: [@neon28](https://github.com/neon28))
