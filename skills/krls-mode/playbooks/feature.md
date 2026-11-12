# Feature

Comportamiento nuevo o cambiado. Tú posees el diseño, delegas la implementación y verificas el resultado.

1. Entiende el terreno antes de diseñar: lee el subsistema afectado (narrow: tú mismo; bulk: subagente read-only). Nombra cómo funciona hoy.
2. Diseña:
   - Nombra la forma del dato central y su estructura organizativa antes de escribir lógica (principio **Dato primero**).
   - Elige el cambio más pequeño que resuelva (principio **Cambio mínimo**). Si hay dos o tres diseños viables y la elección importa, compáralos en una tabla y decide uno.
3. Escribe el checkpoint: qué se paraleliza, qué se serializa y por qué. Si todo va a un solo worker, basta una línea con el porqué.
4. Delega siempre:
   - Toda escritura de código va a un agente `worker` en background, también la trivial (1-2 archivos). Brief standalone: objetivo, paths permitidos, forma del dato, criterios de éxito, cómo verificar, qué reportar, y la ruta absoluta al SKILL.md de krls-mode.
5. Revisa el diff real, no el resumen del worker. Devuelve scope crecido, abstracciones sin causa o comentarios-fase, citando el principio violado. Escribe tu propio resumen del cambio.
6. Verifica en la superficie real (sección Verificación del manual). Antes y después si el cambio altera comportamiento visible. Este paso no admite `skip`.
7. Commits pequeños: una unidad verificada, un commit, la siguiente. Mensajes: skill `krls-git` del proyecto (sección Git del manual). Push solo con permiso del usuario.
8. **Reporte:** qué cambia para el usuario, qué hereda el próximo mantenedor, evidencia pegada (salida real), decisiones abiertas.
