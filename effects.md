| Effect | Descripción |
|----------|-------------|
| `ADD_ATTRIBUTE:attribute:value` | Añade un atributo al jugador. Solo funciona con `EFFECT_STATIC`. |
| `SET_DAMAGE:value` | Establece el daño infligido por `Victim` o `Attacker`. |
| `TELEPORT_LOCATION:x:y:z` | Teletransporta a `Victim` o `Attacker` a coordenadas específicas. |
| `TELEPORT_PLAYER:victim/attacker` | Teletransporta a un jugador hacia su `Victim` o `Attacker`. |
| `BOSSBAR:id:color:style:ticks:text` | Genera una bossbar para el jugador. `ticks` es opcional; si se omite, permanecerá activa indefinidamente. |
| `UPDATE_BOSSBAR:id:text` | Actualiza el texto de una bossbar existente. |
| `RESET_COOLDOWN:enchant` | Reinicia el cooldown de un encantamiento específico. |
| `MARK:name:ticks` | Aplica una marca temporal a `Victim` o `Attacker`. |
| `P_VARIABLE:name:value` | Crea o modifica una variable personal del jugador que porta el encantamiento. |
| `P_INCREMENT_VAR:name:value` | Incrementa o decrementa (si el valor es negativo) una variable personal del jugador. |
