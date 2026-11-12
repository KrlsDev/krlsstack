# Investigation

Pregunta de solo lectura. El entregable es una respuesta con evidencia, no código. Prohibido editar archivos del proyecto.

1. Escribe en una frase la pregunta exacta que vas a responder y para quién.
2. Dimensiona la lectura:
   - Narrow (un módulo, una función, una duda puntual): lee tú mismo.
   - Bulk (subsistema de varios archivos o servicios): lanza un subagente read-only con brief standalone: ángulo, alcance, qué reportar. No cargues el bruto en tu contexto.
3. Investiga. Si la pregunta es sobre comportamiento en runtime, ejecuta comandos o código de solo lectura.
4. Redacta la respuesta con este formato, borrando lo que no aplique:
   - Overview (2-3 frases)
   - Cómo funciona (el flujo, paso a paso)
   - Dónde vive cada cosa (archivo y línea)
   - Gotchas (lo no obvio que muerde)
5. Cada afirmación lleva `archivo:línea` o salida de comando. Lo que no puedas verificar queda etiquetado como conjetura.
6. Si la investigación destapa un bug o un riesgo, repórtalo. No lo arregles: no es este playbook.

**Reporte:** la respuesta del paso 4, más supuestos y preguntas abiertas.
