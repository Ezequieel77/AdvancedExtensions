| Effect                              | Description                                                                                                    |
| ----------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| `EXECUTE_EFFECTS:group_name`        | Executes a predefined group of effects from `effects.yml`. Allows reusable and modular effect logic.         |
| `ADD_ATTRIBUTE:attribute:value`     | Adds an attribute to the player. Only works with `EFFECT_STATIC`.                                              |
| `ADD_ATTRIBUTE_TEMP:attribute:value:seconds` | Temporarily adds an attribute to the player for the specified duration in seconds. |
| `ADD_DAMAGE:value`                  | Adds extra damage to the original damage dealt by the attacker.                                                |
| `BOSSBAR:id:color:style:ticks:text` | Creates a bossbar for the player. `ticks` is optional; if omitted, it will remain active indefinitely.         |
| `JAIL:material:type:radius:height:ticks[:roofAndFloor]` (cuboid)<br>`JAIL:material:type:radius:ticks` (sphere)    | Creates a temporary jail centered on the player's feet. `type` can be `cuboid` or `sphere`. For `cuboid`, builds walls up to `height`, plus a floor and roof by default (set `roofAndFloor` to `false` for walls only); `radius` must be odd, minimum 5. For `sphere`, builds a hollow spherical shell using `radius` and does not accept `height`. |
| `MARK:name:ticks`                   | Applies a temporary mark to `Victim` or `Attacker`.                                                            |
| `P_INCREMENT_VAR:name:value`        | Increments or decrements (if value is negative) a personal variable for the enchantment holder.                |
| `P_VARIABLE:name:value`             | Creates or modifies a personal variable for the enchantment holder.                                            |
| `RESET_COOLDOWN:enchant`            | Resets the cooldown of a specific enchantment.                                                                 |
| `SET_DAMAGE:value`                  | Sets the damage dealt by `Victim` or `Attacker`.                                                               |
| `TELEPORT_LOCATION:x:y:z`           | Teleports `Victim` or `Attacker` to specific coordinates.                                                      |
| `TELEPORT_PLAYER:victim/attacker`   | Teleports a player towards `Victim` or `Attacker`.                                                             |
| `TEMP_BLOCK:type:radius:ticks`      | Places temporary blocks at the feet of `Victim` or `Attacker`. Radius must be odd.                             |
| `UPDATE_BOSSBAR:id:text`            | Updates the text of an existing bossbar.                                                                       |
| `SET_COOLDOWN:enchant:lineIndex:seconds` | Sets the cooldown of a specific effect line within an enchantment. `lineIndex` refers to the effect's position in the enchantment's effect list. |
| `CREATE_ZONE:name:type:radius:ticks[:particle]` | Creates a temporary zone at the target's location. `type` can be `circle` or `square`, `radius` defines the zone size, `ticks` defines its duration, and `particle` is optional and displays particles around the zone perimeter. The zone name can be detected using `%ae_in_zone_<name>%`. |



## MythicMobs Effects

| Effect                       | Description                                                                                              |
| ---------------------------- | -------------------------------------------------------------------------------------------------------- |
| `MM_SKILL:skillname:power` | Executes a MythicMobs skill using the attacker as the caster. power is optional and defaults to 1.0. The target is determined by the selector defined inside the MythicMobs skill itself. If no selector is defined in the skill, the target will be the entity resolved by AE (@Victim, @Attacker, etc.). |
| `MM_SPAWN:mobname:level`   | Spawns a MythicMob at the target's location. `level` is optional and defaults to `1`.                    |


| Detailed list of placeholders [➡️ Placeholders](placeholders.md) |
|-------------------------------------------------------------------|
