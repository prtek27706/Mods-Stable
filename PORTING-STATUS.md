# Mindustry v8 / build 160.5 port status

This working copy targets Mindustry v8 build 160.5 and JDK 17. The workflow is located at `.github/workflows/build.yml`.

## Ammo definition migration

- Removed the obsolete `mindustry.type.ammo.ItemAmmoType` import from `UAWUnitTypes.java`.
- Removed all 10 legacy `UnitType.ammoType = new ItemAmmoType(...)` assignments, which do not exist in the Mindustry v8 API.
- Preserved unit weapon definitions, bullet types, and their `ammoMultiplier` values. These affect weapon/bullet behavior and should not be changed as a substitute for the removed unit-level ammo type.
- Mindustry v8 does not expose the old unit-level `ammoType` field. Therefore, those legacy assignments cannot be translated one-for-one to a current field. Unit weapons use their configured bullet definitions; the old per-unit item restriction is not represented by this API.

## Build requirements

- JDK 17
- Gradle wrapper
- Network access to resolve Mindustry, Arc, and MultiCrafterLib dependencies

## Validation status

The uploaded GitHub Actions log reached `:compileJava` and reported API errors in unit ammo definitions, stat displays, and sound constants. This archive addresses the obsolete unit ammo import and assignments only; the other compiler errors still need to be fixed before a successful build can be expected.

Run `./gradlew clean build` with JDK 17. The port is not yet compile-verified.


## Follow-up fixes from the GitHub Actions build log

- Replaced references to removed vanilla `Sounds` constants with available general-purpose sounds. These are compile-compatibility fallbacks; some sound choices may need later audio polish.
- Replaced removed `ItemDisplay` and `LiquidDisplay` UI classes in `UAWStatValues` with local table-based display helpers that show content icons, quantities, names, and per-second labels.
- The GitHub Actions log did not show remaining unit `ammoType` errors in this run. Unit ammunition behavior still requires gameplay review because the old `UnitType.ammoType` assignments were removed.
- These changes have not yet been verified by a successful Gradle build. Run the workflow again and use the next compiler output to continue the port.


## Compatibility pass 3

- Replaced the remaining unavailable `Sounds.artillery` reference in `UAWUnitTypes.java` with the available `Sounds.shoot` fallback, based on the latest GitHub Actions compiler output.
- The latest build log reported only this missing sound symbol at this stage. Re-run the workflow to reveal any subsequent errors; this is not yet a verified successful build.
