# Trigger List

| Trigger | Description |
|----------|-------------|
| `WORLD_CHANGE` | Executes when changing worlds. |
| `TOTEM_USE` | Executes when using a totem. |
| `ATTACK_ALL` | Executes when hitting any entity in melee. |
| `DEFENSE_ALL` | Executes when taking melee damage from any entity. |
| `DEFENSE_PROJECTILE_ALL` | Executes when hit by a projectile from any entity. |
| `SHOOT_ALL` | Executes when an arrow hits any entity. |
| `BLOCK_PLACE` | Executes when a player places a block. |
| `OUT_OF_COMBAT` | Executes upon leaving combat. The time required to leave combat is defined in `config.yml`. Highly recommended to match it with the combat plugin you are using. |
| `ENTER_COMBAT` | Executes upon entering combat (first hit dealt or received after being out of combat). |
| `ARROW_HIT_BLOCK` | Triggered when an arrow shot by the player hits a block. This trigger also provides the `%arrow_x%`, `%arrow_y%`, and `%arrow_z%` placeholders, containing the impact coordinates. |

| Detailed list of effects and how they work [➡️ Effects](effects.md) |
|----------------------------------------------------------------------|
