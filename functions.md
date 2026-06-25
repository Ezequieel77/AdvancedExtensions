## Functions

Functions allow you to modify how an individual effect line behaves.

Functions can be combined together on the same effect line.

## Cooldown

The `cooldown` function adds an independent cooldown to an effect line.

### Syntax

```yaml
<cooldown>seconds</cooldown>
```

### Example

```yaml
- "ADD_DAMAGE:5 <cooldown>10</cooldown>"
```

The effect can only execute once every 10 seconds.

### Notes

* Cooldowns are tracked per effect line.
* Different effect lines can have different cooldowns.
* Cooldowns respect `~POINTER` and `<condition>` checks and will not start unless the line is eligible to execute.
* Avoid combining `<cooldown>` and `<chance>` on the same effect line. Due to the order in which functions are evaluated, the cooldown system cannot reliably determine whether a chance-based effect will execute without performing an additional random roll, which may lead to inconsistent behavior.
* Enchantment-level chances are fully supported. Using the standard AE `chance:` option on a level is safe and does not interfere with line cooldowns.

### Recommended

```yaml
levels:
  '1':
    chance: 25
    effects:
      - "ADD_DAMAGE:5 <cooldown>10</cooldown>"
```

The enchantment has a 25% chance to activate, and the effect line can only execute once every 10 seconds.

### Not Recommended

```yaml
effects:
  - "ADD_DAMAGE:5 <chance>25</chance> <cooldown>10</cooldown>"
```

This combination may produce inconsistent results and should be avoided.

### Example

```yaml
dash:
  display: "%group-color%Dash"
  description: |-
    Grants a temporary
    burst of speed.
  applies-to: Sword
  type: RIGHT_CLICK
  group: INFERNAL
  applies:
    - ALL_SWORD
  levels:
    "1":
      cooldown: 1
      effects:
        - "MESSAGE:&cYou must wait %ae_line_cooldown_dash_line2% seconds <condition>%ae_line_cooldown_dash_line2% > 0 : %allow%</condition>"
        - "PLAY_SOUND:block.anvil.place <condition>%ae_line_cooldown_dash_line2% > 0 : %allow%</condition>"
        - "BOOST:FORWARD:15 <cooldown>10</cooldown>"
```

In this example, the dash effect has its own 10-second line cooldown.

When the player attempts to use the enchantment while the effect is still on cooldown, a message is displayed showing the remaining cooldown time.

### Understanding Line Indexes

The placeholder format is:

```text
%ae_line_cooldown_<enchant>_line<index>%
```

For example:

```text
%ae_line_cooldown_dash_line2%
```

This placeholder refers to the third effect line in the `dash` enchantment.

Effect line indexes start at `0`:

```yaml
effects:
  - "MESSAGE:..."                    # line0
  - "PLAY_SOUND:block.anvil.place"   # line1
  - "BOOST:FORWARD:15 <cooldown>10</cooldown>" # line2
```

### Important

If you add, remove, or reorder effect lines, the index may change.

For example, adding a new effect above the boost:

```yaml
effects:
  - "MESSAGE:..."                    # line0
  - "PLAY_SOUND:block.anvil.place"   # line1
  - "PARTICLE:FLAME"                 # line2
  - "BOOST:FORWARD:15 <cooldown>10</cooldown>" # line3
```

The cooldown placeholder must also be updated:

```text
%ae_line_cooldown_dash_line3%
```

Otherwise, the placeholder will reference the wrong effect line and may display an incorrect cooldown value.

| SkillBook [➡️ SkillBook](skillbook.md) |
|---------------------------------------------------------------|
