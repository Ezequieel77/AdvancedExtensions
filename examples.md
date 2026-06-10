¿Dónde debo crear los encantamientos?

Una vez el plugin sea instalado en su servidor, lo único que tiene que hacer es ir al archivo AdvancedEnchantments/enchantments.yml y empezar a configurar como normalmente lo hace.

# Implementación de funcionalidades

Intentemos ampliar un encantamiento predeterminado de AdvancedEnchantments mediante las herramientas que ofrece AdvancedExtensions.

```corrupt:
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
Este encantamiento aplica daño periódico al objetivo mediante varias instancias de DO_HARM separadas por intervalos de tiempo.

Utilizando variables personales, detección de combate y bossbars, podemos transformar la mecánica en un sistema de escalado progresivo que recompensa los enfrentamientos prolongados.

```corrupt:
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
        - "INCREASE_DAMAGE:%p_var_combat% <condition>%attacker is holding% contains AXE : %allow%</condition>  ~ATTACK"
        - "P_VARIABLE:combat:0 ~OUT_OF_COMBAT"
        - "UPDATE_BOSSBAR:combat:Additional Damage: 0 ~OUT_OF_COMBAT"
        - "UPDATE_BOSSBAR:combat:Additional Damage: %p_var_combat%% ~REPEATING"
```
En esta versión, el jugador acumula una carga de combate cada 10 segundos mientras permanece en PvP. Cada carga aumenta el daño de las hachas en un 3%, mostrando el valor acumulado mediante una bossbar. Al abandonar el combate, la acumulación se reinicia automáticamente.






