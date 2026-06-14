# Where should I create enchantments?
Once the plugin is installed on your server, all you need to do is go to the `AdvancedEnchantments/enchantments.yml` file and start configuring it as you normally would.

# Implementing features
Let's try to expand a default AdvancedEnchantments enchantment using the tools provided by AdvancedExtensions.

```yaml
corrupt:
  display: '%group-color%Corrupt'
  description: Deals damage over time.
  applies-to: Axes
  type: ATTACK
  group: ULTIMATE
  applies:
  - ALL_AXE
  levels:
    '1':
      chance: 12
      cooldown: 4
      effects:
      - DO_HARM:<random number>2-3</random number> @Victim
      - WAIT:20
      - DO_HARM:<random number>2-3</random number> @Victim
      - WAIT:40
      - DO_HARM:<random number>2-3</random number> @Victim
```

This enchantment applies periodic damage to the target through multiple DO_HARM instances separated by time intervals.

Using personal variables, combat detection and bossbars, we can transform this mechanic into a progressive scaling system that rewards prolonged engagements.

```yaml
corrupt:
  display: '%group-color%Corrupt'
  description: |-
   Deals 3% more damage for every 10 seconds you remain in combat.
   Resets when you leave combat.
   The bonus damage only applies to axes.
  applies-to: Helmet
  type: ATTACK;EFFECT_STATIC;OUT_OF_COMBAT;REPEATING
  group: ULTIMATE
  applies:
  - ALL_HELMET
  levels:
    '1':
      time: 10
      effects:
        - "BOSSBAR:combat:red:solid:Additional Damage: 0 ~EFFECT_STATIC"
        - "P_VARIABLE:combat:0 ~EFFECT_STATIC"
        - "P_INCREMENT_VAR:combat:3 <condition>%ae_in_combat% = true : %allow%</condition> ~REPEATING"
        - "INCREASE_DAMAGE:%p_var_combat% <condition>%attacker is holding% contains AXE : %allow%</condition> ~ATTACK"
        - "P_VARIABLE:combat:0 ~OUT_OF_COMBAT"
        - "UPDATE_BOSSBAR:combat:Additional Damage: 0 ~OUT_OF_COMBAT"
        - "UPDATE_BOSSBAR:combat:Additional Damage: %p_var_combat%% ~REPEATING"
```

In this version, the player accumulates a combat charge every 10 seconds while remaining in PvP. Each charge increases axe damage by 3%, displaying the accumulated value through a bossbar. Upon leaving combat, the accumulation resets automatically.

| Functions [➡️ Functions](functions.md) |
|---------------------------------------------------------------|


