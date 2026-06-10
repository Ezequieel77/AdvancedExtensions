# Lista de Triggers


| Trigger | Descripción |
|----------|-------------|
| ```WORLD_CHANGE``` | Se ejecuta al cambiar de mundo. |
| ```TOTEM_USE``` | Se ejecuta al usar un tótem. |
| ```ATTACK_ALL``` | Fusión de `ATTACK` y `ATTACK_MOB`. |
| ```DEFENSE_ALL``` | Fusión de `DEFENSE` y `DEFENSE_MOB`. |
| ```DEFENSE_PROJECTILE_ALL``` | Fusión de `DEFENSE_PROJECTILE` y `DEFENSE_MOB_PROJECTILE`. |
| ```SHOOT_ALL``` | Fusión de `SHOOT` y `SHOOT_MOB`. |
| ```OUT_OF_COMBAT``` | Se ejecuta al salir de combate. El tiempo necesario para abandonar el combate se define en `config.yml`. Altamente recomendable hacerlo coincidir con el plugin de combate que esté utilizando|
| ```ENTER_COMBAT``` | Se ejecuta al entrar en combate (primer golpe realizado o recibido tras estar fuera de combate). |
