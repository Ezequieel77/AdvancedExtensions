# AdvancedExtensions

AdvancedExtensions es una extensión del plugin AdvancedEnchantments que agrega nuevos efectos, desencadenantes y placeholders, con el objetivo de ampliar las posibilidades que ofrece.

Para comprender esta documentación, es necesario entender el funcionamiento de AdvancedEnchantments.

Sitios oficiales de AdvancedEnchantments:
 * https://wiki.advancedplugins.net/abilities/introduction
 * https://advancedplugins.net/item/AdvancedEnchantments.1


# Características principales

- Nuevos triggers.
- Nuevos placeholders.
- Nuevos effects.

# Y eso hace posible:

- Detección de combate entre jugadores.
- Sistema de marcas temporales.
- Variables personalizadas por jugador.
- Atributos permanentes.
- Bossbars dinámicas.
- Teletransportes avanzados.


# Ejemplo:

Simulación de Ira

Este encantamiento utiliza una variable personal (rage) para almacenar puntos de ira acumulados.

Cada vez que el portador recibe daño, la variable aumenta en 1 punto. Al atacar, el daño infligido aumenta un 5% por cada punto de ira almacenado. Después de ejecutar el golpe, se consumen 5 puntos de ira.

Mientras el jugador permanezca en combate, la ira seguirá acumulándose y consumiéndose dinámicamente. Al salir de combate, la variable se reinicia a 0 automáticamente.

El estado actual de la ira se muestra mediante una bossbar que se actualiza en tiempo real utilizando el placeholder %p_var_rage%.

Variables personales (P_VARIABLE).
Variables incrementales (P_INCREMENT_VAR).
Placeholders personalizados (%p_var_name%).
Bossbars dinámicas (BOSSBAR y UPDATE_BOSSBAR).
Triggers personalizados (OUT_OF_COMBAT).
Operaciones matemáticas dentro de efectos (<math>).

Aunque el ejemplo representa un sistema de ira, la misma lógica puede utilizarse para crear mecánicas de energía, maná, acumulaciones, cargas, combos, corrupción, adrenalina o cualquier otro recurso personalizado.

```ragetest:
  display: "%group-color%Acumulación de Ira"   
  description: |- 
    Aumenta el daño en 5% por
    cada punto de ira acumulado.
    Pierdes 5 puntos de ira por golpe
    infligido.
    Pierdes toda tu ira al salir de 
    combate.
  applies-to: Casco 
  type: ATTACK;EFFECT_STATIC;DEFENSE;REPEATING;OUT_OF_COMBAT
  group: ESPECIAL
  applies:
    - ALL_HELMET
  levels:
    "1":
      time: 2
      effects:
        - "BOSSBAR:rage:red:solid:Ira: 0 ~EFFECT_STATIC"
        - "P_VARIABLE:rage:0 ~EFFECT_STATIC"
        - "P_INCREMENT_VAR:rage:1 ~DEFENSE"
        - "INCREASE_DAMAGE:<math>%p_var_rage% * 5</math> ~ATTACK"
        - "P_INCREMENT_VAR:rage:-5 ~ATTACK"
        - "P_VARIABLE:rage:0 ~ATTACK <condition>%p_var_rage% < 0 : %allow%</condition>"
        - "P_VARIABLE:rage:0 ~OUT_OF_COMBAT"
        - "UPDATE_BOSSBAR:rage:Ira: 0 ~OUT_OF_COMBAT"
        - "MESSAGE:Saliste de combate. ~OUT_OF_COMBAT"
        - "UPDATE_BOSSBAR:rage:Ira: %p_var_rage% ~REPEATING"
        - "UPDATE_BOSSBAR:rage:Ira: %p_var_rage% ~ATTACK"
        - "UPDATE_BOSSBAR:rage:Ira: %p_var_rage% ~DEFENSE"
```

# Explicación línea por línea

* ```"BOSSBAR:rage:red:solid:Ira: 0 ~EFFECT_STATIC"```

  Crea una bossbar exclusiva para el jugador con el texto inicial "Ira: 0". Al ejecutarse mediante EFFECT_STATIC, permanecerá activa hasta que la pieza con el encantamiento sea desequipada.

* ```"P_VARIABLE:rage:0 ~EFFECT_STATIC"```

  Crea una variable personal llamada "rage" con valor inicial 0. Al igual que la bossbar, existirá mientras el jugador mantenga equipada la pieza con el encantamiento.

* ```"P_INCREMENT_VAR:rage:1 ~DEFENSE"```

  Cada vez que se active el trigger DEFENSE, incrementa en 1 el valor de la variable "rage".

* ```"INCREASE_DAMAGE:<math>%p_var_rage% * 5</math> ~ATTACK"```

  Al activarse ATTACK, aumenta el daño infligido en función del valor actual de "rage" multiplicado por 5. Por ejemplo, si "rage" vale 5, el daño aumentará un 25%.

* ```"P_INCREMENT_VAR:rage:-5 ~ATTACK"```

  Después de aplicar el daño potenciado, consume 5 puntos de ira.

* ```"P_VARIABLE:rage:0 ~ATTACK <condition>%p_var_rage% < 0 : %allow%</condition>"```

  Si la reducción anterior provoca que la variable quede por debajo de 0, su valor se corrige automáticamente a 0.

* ```"P_VARIABLE:rage:0 ~OUT_OF_COMBAT"```

  Reinicia la variable al activarse OUT_OF_COMBAT, eliminando toda la ira acumulada.

* ```"UPDATE_BOSSBAR:rage:Ira: 0 ~OUT_OF_COMBAT"```

  Actualiza inmediatamente la bossbar al abandonar el combate para reflejar el reinicio de la variable.

* ```"MESSAGE:Saliste de combate. ~OUT_OF_COMBAT"```

  Envía una notificación al jugador cuando abandona el combate. Esta línea es opcional y se utiliza únicamente como referencia visual para el ejemplo.

* ```"UPDATE_BOSSBAR:rage:Ira: %p_var_rage% ~REPEATING"```

  Actualiza periódicamente el texto de la bossbar utilizando el valor actual de la variable. La frecuencia de actualización se define mediante la opción "time". En este ejemplo, cada 2 segundos.

* ```"UPDATE_BOSSBAR:rage:Ira: %p_var_rage% ~ATTACK"```

  Fuerza una actualización inmediata tras atacar para evitar que la bossbar espere al siguiente ciclo de REPEATING.

* ```"UPDATE_BOSSBAR:rage:Ira: %p_var_rage% ~DEFENSE"```

  Cumple la misma función que la línea anterior, pero cuando el jugador recibe daño.


|------------|-------------|
|[➡️ Triggers](triggers.md) |
|----------|-------------|













        
