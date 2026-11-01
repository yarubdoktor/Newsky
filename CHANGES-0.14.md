# IRON-FRONT 0.14 – Battlefield Immersion

## Collective threat response
- When an enemy unit damages any friendly combat unit, the hostile attacker with the strongest current threat count becomes the shared response target.
- All living friendly units with a combat weapon join the response, including units that were moving or idle.
- Workers and logistics vehicles with no combat capability are not pulled into combat.
- Explicit orders to attack the enemy HQ or a specific structure are preserved.
- Shared unit targets are prioritized over opportunistic nearby targets while in weapon range, keeping the squad focused.
- If the attacker is destroyed before the response is assigned, no stale target order is created.

## Battlefield presentation
- Added deterministic shell craters and scattered debris as cosmetic terrain dressing; they do not block navigation or alter movement.
- Extended heavy-weapon impact lifetimes and added larger impact rings, brief blast glow and rising smoke puffs for tanks and artillery.
- Existing camera, touch controls, movement, selection and map navigation are unchanged.

## Verification
- Added simulation tests for squad-wide focus fire, logistics exclusion and preservation of explicit HQ attack orders.
- Web tests, production build and Android APK build are run by the 0.14 GitHub Actions workflow.
- Final visual/performance acceptance still requires testing on the user's Android device.
