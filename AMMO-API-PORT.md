# Mindustry v8 ammo API audit

Target: Mindustry v8, build 160.5, Java 17.

## Findings

- Item turret definitions in `src/UAW/content/blocks/UAWBlocksDefence.java` use the `ItemTurret.ammo(Object... itemBulletPairs)` API. This API remains available in v8 and populates `ammoTypes`; these calls should not be mechanically rewritten.
- `UAWItemTurret.java` reads `ammoTypes` for its custom ammo-stat display. The map is still part of the v8 `ItemTurret` API.
- Unit definitions use `mindustry.type.ammo.ItemAmmoType` and do not use the removed `AmmoTypes` helper or the removed `ContentType.ammo` content type.
- No source matches were found for `AmmoTypes`, `new AmmoType(...)`, or `ContentType.ammo`.

## Porting rule

Preserve each item's bullet mapping and all `BulletType` properties. Only change ammo code when a build error identifies an API that actually changed. The remaining build is still needed to find unrelated v8 API incompatibilities.
