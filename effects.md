| Effect | Description |
|----------|-------------|
| `ADD_ATTRIBUTE:attribute:value` | Adds an attribute to the player. Only works with `EFFECT_STATIC`. |
| `SET_DAMAGE:value` | Sets the damage dealt by `Victim` or `Attacker`. |
| `TELEPORT_LOCATION:x:y:z` | Teleports `Victim` or `Attacker` to specific coordinates. |
| `TELEPORT_PLAYER:victim/attacker` | Teleports a player towards `Victim` or `Attacker`. |
| `TEMP_BLOCK:type:radius:ticks` | Places temporary blocks at the feet of `Victim` or `Attacker`. Radius must be odd. |
| `JAIL:material:xz:height:ticks` | Creates a roofless jail around the player from their feet up to the defined height. xz must be odd, minimum 5. |
| `BOSSBAR:id:color:style:ticks:text` | Creates a bossbar for the player. `ticks` is optional; if omitted, it will remain active indefinitely. |
| `UPDATE_BOSSBAR:id:text` | Updates the text of an existing bossbar. |
| `RESET_COOLDOWN:enchant` | Resets the cooldown of a specific enchantment. |
| `MARK:name:ticks` | Applies a temporary mark to `Victim` or `Attacker`. |
| `P_VARIABLE:name:value` | Creates or modifies a personal variable for the enchantment holder. |
| `P_INCREMENT_VAR:name:value` | Increments or decrements (if value is negative) a personal variable for the enchantment holder. |


## MythicMobs Effects

| Effect                       | Description                                                                                              |
| ---------------------------- | -------------------------------------------------------------------------------------------------------- |
| `MM_SKILL:skillname:power` | Executes a MythicMobs skill using the attacker as the caster. `power` is optional and defaults to `1.0`. |
| `MM_SPAWN:mobname:level`   | Spawns a MythicMob at the target's location. `level` is optional and defaults to `1`.                    |


| Detailed list of placeholders [➡️ Placeholders](placeholders.md) |
|-------------------------------------------------------------------|
