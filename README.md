# AdvancedExtensions

AdvancedExtensions is an extension of the AdvancedEnchantments plugin that adds new effects, triggers and placeholders, with the goal of expanding the possibilities it offers.

To understand this documentation, you need to understand how AdvancedEnchantments works.

Official AdvancedEnchantments sites:
* https://wiki.advancedplugins.net/abilities/introduction
* https://advancedplugins.net/item/AdvancedEnchantments.1

# Main features

- New triggers.
- New placeholders.
- New effects.

# And that makes possible:

- Player combat detection.
- Temporary mark system.
- Per-player custom variables.
- Permanent attributes.
- Dynamic bossbars.
- Advanced teleportation.

# Example:

Rage Simulation

This enchantment uses a personal variable (rage) to store accumulated rage points.

Every time the holder takes damage, the variable increases by 1 point. When attacking, the damage dealt increases by 5% per stored rage point. After landing the hit, 5 rage points are consumed.

While the player remains in combat, rage will keep accumulating and being consumed dynamically. Upon leaving combat, the variable resets to 0 automatically.

The current rage state is displayed through a bossbar that updates in real time using the placeholder %p_var_rage%.

- Personal variables (P_VARIABLE).
- Incremental variables (P_INCREMENT_VAR).
- Custom placeholders (%p_var_name%).
- Dynamic bossbars (BOSSBAR and UPDATE_BOSSBAR).
- Custom triggers (OUT_OF_COMBAT).
- Math operations inside effects (\<math>).

Although the example represents a rage system, the same logic can be used to create energy, mana, stacks, charges, combos, corruption, adrenaline or any other custom resource mechanic.

```yaml
ragetest:
  display: "%group-color%Rage Accumulation"
  description: |-
    Increases damage by 5% per
    accumulated rage point.
    Lose 5 rage points per
    attack landed.
    Lose all rage upon leaving
    combat.
  applies-to: Helmet
  type: ATTACK;EFFECT_STATIC;DEFENSE;REPEATING;OUT_OF_COMBAT
  group: SPECIAL
  applies:
    - ALL_HELMET
  levels:
    "1":
      time: 2
      effects:
        - "BOSSBAR:rage:red:solid:Rage: 0 ~EFFECT_STATIC"
        - "P_VARIABLE:rage:0 ~EFFECT_STATIC"
        - "P_INCREMENT_VAR:rage:1 ~DEFENSE"
        - "INCREASE_DAMAGE:<math>%p_var_rage% * 5</math> ~ATTACK"
        - "P_INCREMENT_VAR:rage:-5 ~ATTACK"
        - "P_VARIABLE:rage:0 ~ATTACK <condition>%p_var_rage% < 0 : %allow%</condition>"
        - "P_VARIABLE:rage:0 ~OUT_OF_COMBAT"
        - "UPDATE_BOSSBAR:rage:Rage: 0 ~OUT_OF_COMBAT"
        - "MESSAGE:You left combat. ~OUT_OF_COMBAT"
        - "UPDATE_BOSSBAR:rage:Rage: %p_var_rage% ~REPEATING"
        - "UPDATE_BOSSBAR:rage:Rage: %p_var_rage% ~ATTACK"
        - "UPDATE_BOSSBAR:rage:Rage: %p_var_rage% ~DEFENSE"
```

# Line by line explanation

* `"BOSSBAR:rage:red:solid:Rage: 0 ~EFFECT_STATIC"`

  Creates a player-exclusive bossbar with the initial text "Rage: 0". Since it runs via EFFECT_STATIC, it will remain active until the enchanted piece is unequipped.

* `"P_VARIABLE:rage:0 ~EFFECT_STATIC"`

  Creates a personal variable named "rage" with an initial value of 0. Like the bossbar, it will exist as long as the player keeps the enchanted piece equipped.

* `"P_INCREMENT_VAR:rage:1 ~DEFENSE"`

  Every time the DEFENSE trigger activates, increments the "rage" variable by 1.

* `"INCREASE_DAMAGE:<math>%p_var_rage% * 5</math> ~ATTACK"`

  When ATTACK triggers, increases damage dealt based on the current value of "rage" multiplied by 5. For example, if "rage" is 5, damage will increase by 25%.

* `"P_INCREMENT_VAR:rage:-5 ~ATTACK"`

  After applying the boosted damage, consumes 5 rage points.

* `"P_VARIABLE:rage:0 ~ATTACK <condition>%p_var_rage% < 0 : %allow%</condition>"`

  If the previous reduction causes the variable to drop below 0, its value is automatically corrected to 0.

* `"P_VARIABLE:rage:0 ~OUT_OF_COMBAT"`

  Resets the variable when OUT_OF_COMBAT triggers, clearing all accumulated rage.

* `"UPDATE_BOSSBAR:rage:Rage: 0 ~OUT_OF_COMBAT"`

  Immediately updates the bossbar upon leaving combat to reflect the variable reset.

* `"MESSAGE:You left combat. ~OUT_OF_COMBAT"`

  Sends a notification to the player when they leave combat. This line is optional and used only as a visual reference for the example.

* `"UPDATE_BOSSBAR:rage:Rage: %p_var_rage% ~REPEATING"`

  Periodically updates the bossbar text using the current variable value. The update frequency is defined by the "time" option. In this example, every 2 seconds.

* `"UPDATE_BOSSBAR:rage:Rage: %p_var_rage% ~ATTACK"`

  Forces an immediate update after attacking to prevent the bossbar from waiting for the next REPEATING cycle.

* `"UPDATE_BOSSBAR:rage:Rage: %p_var_rage% ~DEFENSE"`

  Serves the same purpose as the previous line, but when the player takes damage.

---

| Detailed list of triggers and how they work [➡️ Triggers](triggers.md) |
|------------------------------------------------------------------------|













        
