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
