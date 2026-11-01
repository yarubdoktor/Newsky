# IRON-FRONT 0.15 — Base spacing and resource mines

## Base layout
- Reworked the construction plot grid to provide wider spacing between buildings.
- Added footprint-clearance checks so new structures are not placed inside an existing structure's reserved space.
- Repositioned the starting barracks to separate it clearly from the HQ.
- Kept the original HQ position, camera, touch controls, unit movement, selection, combat and map navigation unchanged.

## Resource mines
- Added six resource mines around each base (12 total across both factions).
- Each mine has a stable ID and its own finite steel, fuel, power and ammunition stock.
- Workers and haul trucks are distributed across the mine sites, remember their assigned mine, and switch to another live mine when their current site is exhausted.
- Mines can be tapped on the 3D battlefield to inspect their remaining resources; selected mines receive a highlight.
- Updated the radar minimap to show the separate friendly and hostile mine locations.
- Expanded save validation for 12 mines and preserved compatibility with older saves that contain two mines or no mine IDs.

## Verification
- Added tests for six mines per faction, mirrored mine placement, building footprint clearance, worker distribution and older-save compatibility.
- The GitHub Actions workflow runs the simulation test suite, production web build and Android APK build.
- Final touch-response, visual-spacing and device-performance acceptance still requires testing on the user's Android device.
