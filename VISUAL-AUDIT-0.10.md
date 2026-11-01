# IRON-FRONT 0.10 — Visual Audit & Asset Roadmap

## Audit baseline
- Repository: `yarubdoktor/Newsky`
- Audited branch: `iron-front-combat-1.0`
- Visual work branch: `iron-front-visual-1.0` (branched from the combat branch; main is untouched)
- Audited source: `IRON-FRONT-0.10-SOURCE.zip`, built from the 0.9 source plus the 0.10 combat patch.
- Engine/rendering: React + TypeScript + Vite + Three.js / React Three Fiber, packaged for Android with Capacitor.
- Battlefield is a real-time 3D WebGL scene. The project has no authored GLB/GLTF/FBX/OBJ models and no standalone image texture files. Buildings, units, terrain props and several effects are currently assembled from Three.js primitive geometries and flat materials.
- Build target is a self-contained HTML; imported assets must remain bundleable and mobile-friendly.

## Existing systems to preserve
- Do not change touch controls, unit selection, movement orders, camera pan/zoom, camera bounds, minimap camera jumps, or manual HQ/building attack commands.
- Keep existing game simulation, unit IDs/types, building IDs/types, navigation coordinates, hit areas, selection rings, health bars, faction visibility, and combat rules.
- Visual models are a rendering layer only. They must not change hit boxes, movement speed, range, collision/navigation or game balance.
- Keep the 0.10 combat behavior: attacker-specific retaliation and unit-only automatic retaliation.
- Keep the current three-biome map layout and the three river bridges/chokepoints.

## Confirmed current asset inventory

### Units — 14 visual variants required
1. Rifle infantry squad
2. Sniper
3. Combat engineer
4. Anti-armor infantry
5. Recon vehicle
6. Main battle tank
7. Heavy tank
8. Armored personnel carrier
9. Self-propelled artillery
10. Attack helicopter
11. Reconnaissance drone
12. Supply truck
13. Mine laborer / worker
14. Haul truck

Suggested reuse: four infantry role variants can share a common humanoid rig/base proportions while retaining distinct weapon, backpack, helmet and equipment silhouettes. Vehicle models should share material palettes and wheel/track components, not the same silhouette.

### Buildings — 14 visual variants required
1. Command HQ
2. Field barracks
3. Power station
4. Fuel refinery
5. Armored factory
6. Research center
7. Watchtower
8. Field hospital
9. Munitions depot
10. Vehicle works
11. Air command / airfield
12. Missile defense / SAM site
13. Destructible barrier wall segment
14. Command relay

The wall segment is one authored model instanced repeatedly (up to the existing ten-segment limit). Both factions reuse the same architecture with faction material variants. Building health/progress/selection overlays stay separate from the model.

### Battlefield / terrain
- 3 ground material sets: forest/temperate, desert, snow.
- 1 river/water surface with biome-compatible tint and material.
- 1 bridge asset, instanced at the existing 3 crossing coordinates.
- 4 mountain/cliff choke-point pieces, with reusable rock variants.
- 4–6 tree silhouettes, plus low-cost bush/grass/ground-clutter variants. Current scene places up to 110 tree instances.
- 4 rock variants, reused across the 8 existing rock placements.
- 1 mine structure with resource-node variants, used at both faction mine positions.
- 1 capture/depot prop family for the 3 central zones.
- 1 rally flag / marker family.
- Road, haul-road, track, crater and terrain-edge decals.
- Preserve current river position, bridge coordinates, mountain chokepoints, mine coordinates, rally position and battlefield bounds.

### Combat / environment effects
1. Small-arms muzzle flash and tracer
2. Bullet impact spark/dust
3. Anti-armor rocket/missile trail and impact
4. Tank cannon flash, shell travel and blast
5. Artillery shell arc, ground burst and temporary crater
6. Explosion burst with debris
7. Fire and layered smoke for damaged/destroyed buildings
8. Damage smoke for heavily damaged vehicles
9. Vehicle exhaust and movement dust
10. Infantry footstep dust
11. Helicopter rotor animation and rotor-wash dust
12. Rain/snow weather particles and ambient wind cues

Existing shot tracers, muzzle flash, impact ring and weather particles are retained and upgraded incrementally.

### Shared visual/UI assets
- 28 unit/building icon illustrations (14 unit + 14 building types), preferably generated from the same model renders.
- Faction decals, unit insignia, warning stripes, windows, doors, antennas, lights, road markings and map labels.
- Shared PBR material palette: painted military metal, bare steel, concrete, rubber, glass, canvas, sand, foliage, snow and water.

## Art direction
Modern military RTS, semi-realistic stylized low-poly: strong recognizable silhouettes, believable proportions and equipment, restrained weathering, faction-specific olive/charcoal versus rust-red/sand accents, readable from the current elevated mobile camera. Avoid photorealistic micro-detail that disappears at battlefield zoom.

## Technical delivery requirements
- Phase 1 uses optimized in-engine procedural mesh models, so no external model downloads are required. Imported GLB (glTF 2.0) assets remain an option for later phases when they provide a measurable quality benefit.
- Coordinate convention: Y-up; ground plane at Y=0; unit forward axis +Z; match current scene orientation.
- Unit models must fit existing logical footprints and preserve invisible touch hit areas.
- Buildings must fit existing placement footprints and preserve their click targets.
- Keep shared materials and instancing where possible.
- Add low-detail LODs / simplified distant silhouettes where they materially reduce mobile draw calls.
- Keep total embedded visual payload small enough for the single-file Vite build and Android APK; target a first visual pack below 8 MB compressed, then measure actual output.
- Validate npm tests, TypeScript/Vite build, APK build, asset loading, mobile viewport and FPS before declaring a phase complete.

## Phased implementation

### Phase 0 — Audit and asset pipeline (this document)
- Confirmed current source, scene structure, visual placeholders, exact inventory and preservation constraints.
- Create a model manifest and reusable in-engine mesh construction/material palette.

### Phase 1 — Army visual pack
- Build and integrate all 14 unit visual variants.
- Add faction palette variants, role-specific weapons/equipment, rotor/track/wheel details and simple idle/movement presentation.
- Preserve every existing unit hit area, ring, health bar and touch interaction.

### Phase 2 — Base and building pack
- Build and integrate all 14 building variants, including the repeatable wall segment.
- Add readable faction palettes, doors, roofs, vents, antennae, lights, signage and construction-stage visual treatment.
- Preserve all building positions, selection and attack interactions.

### Phase 3 — Terrain and battlefield pack
- Upgrade ground materials for the three biomes, river, bridges, cliffs, rocks, forests, mines, depots, roads and decals.
- Preserve the tactical map layout and navigation obstacles exactly.

### Phase 4 — Combat VFX and environmental animation
- Upgrade weapon-specific firing, impacts, explosions, smoke/fire, damage states, dust, rotor wash and weather.
- Add visual-only animation; no simulation or combat-stat changes.

### Phase 5 — Polish, optimization and release verification
- LODs, instancing, draw-call/material optimization, mobile FPS checks, Android APK build, and before/after visual review.

## Status
Phase 0 audit is complete. Phase 1 now has 14 role-specific in-engine unit models integrated in the source patch on `iron-front-visual-1.0`. GitHub Actions passed the full npm test suite and production web build. Android wrapper/APK packaging is still running; physical-phone FPS and visual review remain pending.
