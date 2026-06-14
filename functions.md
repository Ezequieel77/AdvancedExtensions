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

