# Controller change history

## October 4, 2026 — Consolidate physical button code

Added the existing production controller program, serial diagnostic, measured
pin mapping, and installation guide to BMO-Ai-Assistant-32proto-firmware-.
Included exact copies of the Pi application file and its controller tests under
`raspberry_pi/`, with instructions for use in the complete BMO application.
No controller or application behavior was changed for this upload.

## October 2, 2026 — Separate controller repository

Copied the existing production firmware and diagnostic program from the BMO
application repository without changing either Python file. Added standalone
installation instructions and links to the BMO application's key handlers.
The owner requested a public repository for this code.

## October 2, 2026 — Correct the USB key range

The controller logged physical button presses, but Linux received no keyboard
events. Inspection of the connected CircuitPython 5.2 USB descriptor found
keyboard usage and logical maxima of 0x65. The original F13–F19 key usages
(0x68–0x6e) were outside that range.

The program now uses F6–F12 (0x3f–0x45). It was installed on the Feather,
compared with the repository copy, and observed automatically reloading.
Raw Linux input tests with BMO closed confirmed press and release for all seven
controls. The owner later confirmed the application button actions worked.

One test registered Down and Left together, followed by a clean separate Left
press. The cause of the overlap was not established. No CircuitPython upgrade
was performed.

## September 30, 2026 — Identify wiring and implement firmware

The connected board identified itself as an Adafruit Feather M0 Basic running
CircuitPython 5.2.0. Switch inputs were measured individually with USB input
and serial diagnostics. The measured pin mapping differed from the supplied
Gerber design, so the measured values were used.

The production program enables internal pull-ups, treats a switch to ground as
a press, debounces for 25 ms, supports the USB keyboard's six-key report limit,
logs transitions over serial, and retries reports after an OSError.
`diagnostic.py` was retained for future pin discovery.

The initial F13–F19 mapping was superseded by the October 2 correction above.
