# Solve

Defecto reportado o refactor. Tú posees el diagnóstico y la decisión, delegas la solución y verificas el resultado.

1. Investiga antes de tocar nada: reproduce el defecto o caracteriza el código actual. Narrow: tú mismo. Bulk: subagente read-only con brief standalone: ángulo, alcance, qué reportar. Traza cada síntoma al primer lugar donde el sistema se equivocó (principio **Causas raíces**).
2. Diseña la solución menos chapuza:
   - Elige el cambio más pequeño que resuelve de verdad (principio **Cambio mínimo**). Mínimo no es chapuza: un guard que esconde el síntoma no es un fix.
   - Si dudas entre una ñapa que evita una gran refactorización y refactorizar bien: para y pregunta al usuario. Es una decisión de arquitectura que ningún experimento resuelve.
   - En refactor: sin cambio de comportamiento. Caracteriza el comportamiento actual antes de mover nada (tests o verificación equivalente) y verifica la equivalencia al final.
3. Escribe el checkpoint: qué se paraleliza, qué se serializa y por qué. Si todo va a un solo worker, basta una línea con el porqué.
4. Delega siempre:
   - Toda escritura de código va a un agente `worker` en background, también la trivial (1 archivo). Brief standalone: objetivo, paths permitidos, forma del dato, criterios de éxito, cómo verificar —incluida la skill `verify` del proyecto—, qué reportar (PASS / ISSUES / BLOCKED + evidencia) y la ruta absoluta al SKILL.md de krls-mode.
   - El worker verifica su propio trabajo con `verify` antes de reportar. PASS o BLOCKED, nunca "creo que funciona".
5. Worker BLOCKED: no lo rebotes tal cual. Revisa su evidencia: brief ambiguo o enfoque equivocado → re-lanza con brief corregido. Dos BLOCKED seguidos → vuelve al paso 2.
6. Revisa el diff real, no el resumen del worker. Devuelve scope crecido, abstracciones sin causa o comentarios-fase, citando el principio violado. Escribe tu propio resumen del cambio.
7. Verifica en la superficie real con el mismo procedimiento que Feature (sección Verificación del manual). Antes y después si el defecto era visible. Este paso no admite `skip`.
8. Commits pequeños: una unidad verificada, un commit, la siguiente. Mensajes: skill `krls-git` del proyecto (sección Git del manual). Push solo con permiso del usuario.
9. **Reporte:** causa raíz encontrada, qué cambia para el usuario, qué hereda el próximo mantenedor, evidencia pegada (salida real), decisiones abiertas.
