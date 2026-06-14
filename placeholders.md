# Placeholder List

| Placeholder | Description |
|-------------|-------------|
| `%distance_damage%` | Returns the distance between `Victim` and `Attacker`. |
| `%ae_enemies_10%` | Returns the number of hostile players (`isDamageable`) within a radius of 10 blocks. |
| `%ae_attribute_attribute%` | Returns the value of a specific attribute of `Victim` or `Attacker`. |
| `%ae_in_combat%` | Returns `true` if the player is in PvP combat; otherwise, `false`. |
| `%ae_has_mark_name%` | Returns `true` if the trigger activator has the specified mark. |
| `%ae_vmark_name%` | Returns `true` if `Victim` has the specified mark. |
| `%ae_amark_name%` | Returns `true` if `Attacker` has the specified mark. |
| `%ae_cooldown_<enchant>%` | Returns the remaining cooldown of the specified enchantment. Replace `<enchant>` with the enchantment's internal name. |
| `%p_var_name%` | Returns the value of a personal variable for the enchantment holder. |
| `%is_mythicmob%` | Returns `true` if the target entity is a MythicMob; otherwise, `false`. |
| `%mm_mob_name%` | Returns the internal MythicMob name of the target entity. Returns an empty string if the entity is not a MythicMob. |
| `%ae_line_cooldown_<enchant>_line<index>%` | Returns the remaining cooldown of a specific effect line within an enchantment. Replace `<enchant>` with the enchantment's internal name and `<index>` with the effect line index. |
| `%ae_in_zone_<name>%` | Returns whether the player is currently inside the specified zone. Replace `<name>` with the zone name defined in `CREATE_ZONE`. |

| How do I implement this? [➡️ Examples](examples.md) |
|---------------------------------------------------------------|
