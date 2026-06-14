# Functions

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

### Combined Example

```yaml
- "ADD_DAMAGE:5 <chance>25</chance> <cooldown>10</cooldown>"
```

The effect has a 25% chance to trigger and can only execute once every 10 seconds.

### Line Cooldowns

Line cooldowns can be accessed using:

```text
%ae_line_cooldown_<enchant>_line<index>%
```

Example:

```text
%ae_line_cooldown_corrupt_line0%
```

Returns the remaining cooldown of line `0` in the `corrupt` enchantment.

## Chance

### Syntax

```yaml
<chance>value</chance>
```

### Example

```yaml
- "ADD_DAMAGE:5 <chance>25</chance>"
```

The effect has a 25% chance to execute.

## Condition

### Syntax

```yaml
<condition>expression : %allow%</condition>
```

### Example

```yaml
- "ADD_DAMAGE:5 <condition>%victim health% > 10 : %allow%</condition>"
```

The effect will only execute if the condition is met.

