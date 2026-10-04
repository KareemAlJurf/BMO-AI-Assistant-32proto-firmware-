# Raspberry Pi button actions

`agent_hailo.py` and `tests/unit/test_controller.py` are exact copies from
[BMO-AI-Assistant-project, commit fea36d0a5eb6eae02fd87d930272cf3f7b42e9b4](https://github.com/KareemAlJurf/BMO-AI-Assistant-project/tree/fea36d0a5eb6eae02fd87d930272cf3f7b42e9b4).
The application keeps its controller handlers in the main GUI file, so the
complete file is included to preserve the working implementation.

## Install

1. Install the full BMO application and its dependencies using that project's
   `LOCAL_SETUP.md`. The source commit above already includes these button actions.
2. If restoring these files into that version of the application, back up its
   existing files and copy `agent_hailo.py` into the application root and
   `tests/unit/test_controller.py` into its matching test directory.
3. Install this repository's root `code.py` on the Feather's CIRCUITPY drive.
4. Restart BMO and keep its window focused to receive button presses.

This directory is an integration snapshot. Running the GUI requires the full
application's `core/` modules, assets, models, dependencies, and configuration.
Do not copy these Pi files to the Feather. Avoid replacing a newer application's
GUI file without comparing changes first.

## Included behavior

- F6: triangle requests a random thought.
- F7: small circle toggles output mute while leaving the microphone enabled.
- F8: big circle listens after 450 ms; a second press within that window quits.
- F9 / F10: volume up / down, with a three-second overlay dismissal.
- F11: stop music and cancel pending song starts.
- F12: play a random song when available and unmuted.
- Held-key suppression, focus-loss cleanup, and legacy F13–F19 aliases.
- Prerecorded audio volume handling and removal of touchscreen mute shortcuts.

The existing tests exercise these behaviors without starting the GUI or audio
hardware. With pytest and numpy installed, run from this repository's root:

```sh
python3 -P -m pytest raspberry_pi/tests/unit/test_controller.py
```

The `-P` option (Python 3.11+) keeps the repository root off Python's import
path so the Feather's `code.py` does not shadow the standard library `code` module.

The source history records successful physical key tests for all seven switches
and owner confirmation of the initial application actions. The later volume
and quit-gesture refinements still require confirmation on the device.
