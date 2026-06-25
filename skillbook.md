# Skill Book

The Skill Book is a configurable item that allows players to activate enchantment skills through a GUI.

Any enchantment with the `ACTIVE_SKILL` type will automatically appear in the Skill Book while it is equipped by the player.

To create an active skill, three steps are required:

Obtaining the Skill Book

Use the following command to give a player a Skill Book:

/aex giveitem <player> skillbook [amount]

Once obtained, right-click the Skill Book to open the active skills menu.

### 1. Configure the skill cooldown

In `config.yml`, register the enchantment and define its cooldown in seconds.

```yaml
active-enchants:
  # enchant: cooldown (in seconds)
  domain: 60
```

### 2. Mark the enchantment as an active skill

Add the `ACTIVE_SKILL` type and execute your effects using the `ACTIVE_SKILL` trigger.

```yaml
domain:
  type: ATTACK_ALL;DEFENSE_ALL;ACTIVE_SKILL

  levels:
    "1":
      effects:
        - "EXECUTE_EFFECTS:domain ~ACTIVE_SKILL"
```

When the player clicks the skill inside the Skill Book, the `ACTIVE_SKILL` trigger is fired.

### 3. Define the skill behavior

The triggered effects can perform any supported actions.

Example:

```yaml
effect-groups:
  domain:
    - "MESSAGE:&Domain expansion!"
    - "CREATE_ZONE:domain:circle:16:200:ANGRY_VILLAGER"
    - "JAIL:DEEPSLATE_BRICK_WALL:sphere:16:200"
    - "BOSSBAR:domain:purple:solid:200:Domain duration: 9s"
    - "WAIT:20"
    - "UPDATE_BOSSBAR:domain:Domain duration: 8s"
    - "WAIT:20"
    - "UPDATE_BOSSBAR:domain:Domain duration: 7s"
    - "WAIT:20"
    - "UPDATE_BOSSBAR:domain:Domain duration: 6s"
    - "WAIT:20"
    - "UPDATE_BOSSBAR:domain:Domain duration: 5s"
    - "WAIT:20"
    - "UPDATE_BOSSBAR:domain:Domain duration: 4s"
    - "WAIT:20"
    - "UPDATE_BOSSBAR:domain:Domain duration: 3s"
    - "WAIT:20"
    - "UPDATE_BOSSBAR:domain:Domain duration: 2s"
    - "WAIT:20"
    - "UPDATE_BOSSBAR:domain:Domain duration: 1s"
    - "WAIT:20"
    - "UPDATE_BOSSBAR:domain:Domain duration: 0s"
```

This example creates a combat arena by:

* Displaying a message.
* Creating a temporary zone.
* Building a spherical jail around the player.
* Displaying a boss bar that updates until the skill ends.

The player can activate the skill again only after the configured cooldown has expired.
