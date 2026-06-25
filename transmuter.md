# Enchant Transmuter

The Enchant Transmuter is a configurable item that allows players to transform an enchantment book into another random enchantment from the same group.

## Obtaining an Enchant Transmuter

Use the following command:

```text
/aex giveitem <player> transmuter [amount] [chance] [group]
```

* `amount` *(optional)* — Number of Transmuters to give.
* `chance` *(optional)* — Success chance of the Transmuter.
* `group` *(optional)* — Enchantment group the Transmuter can be used on.

If `chance` and `group` are omitted, both values are generated randomly according to the configuration in `items.yml`.

## Configuration

Example:

```yaml
transmuter:
  material: NETHER_STAR
  name: "&5&lEnchant Transmuter &8[&d{chance}%&8] &8[&5{group}&8]"
  lore:
    - "Drag this item onto an enchantment"
    - "to transmute it into a random enchantment."
    - ""
    - "&d{chance}% &7success rate"
    - "&5Group: &f{group}"
    - ""
    - "&cOn fail: book is destroyed"
  destroy-book-on-fail: true
  min-chance: 10
  max-chance: 45
```

## How it works

* Drag the Transmuter onto a single enchantment book.
* The book must belong to the same enchantment group as the Transmuter.
* If the transmutation succeeds, the enchantment is replaced with a random enchantment from the same group.
* If it fails, the configured failure behavior is applied.
