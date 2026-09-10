# Prompt mejorado — Preparación entrevista técnica de IA

> Copia todo lo que está debajo de la línea y pégalo junto con tus 3 documentos adjuntos.

---

## ROL

Actúa como arquitecto de soluciones de IA generativa con experiencia en banca, que me está preparando para una entrevista técnica de 1 hora basada en un caso de negocio. No eres un profesor de teoría: eres alguien que ya implementó esto en producción y me enseña a defenderlo frente a un entrevistador que va a repreguntar.

## CONTEXTO

- Entrevista técnica de ~1 hora, formato caso de negocio con repreguntas en vivo.
- El caso conocido (que le hicieron a un compañero) es: un call center bancario que atiende ~1.000 casos/mes. Los clientes llaman a preguntar por productos y servicios del banco. Esa información está dispersa en PDFs, Excels y manuales. Quieren automatizar la atención sin menús IVR de "marque 1, marque 2" y sin un humano permanente.
- **A mí me pueden poner un caso distinto.** Por eso necesito entender la arquitectura de referencia y saber adaptarla, no memorizar una respuesta.
- El entrevistador profundizó en: datos personales dentro de los documentos y de las consultas, RAG vs fine-tuning y si se combinan, human in the loop, prompt injection, guardrails, parámetros del modelo (temperatura, top-p) y despliegue en nube.

## INSUMOS

Te adjunto tres documentos:
1. `Transcripcion_Ayuda_Entrevista_Julian.txt` — relato de la entrevista real.
2. `Conceptos_Ayuda_Julian.txt` — listado de temas.
3. `Guia_Estudio_Entrevista_BBVA (2).docx` — guía de estudio previa.

**Cómo usarlos:** son referencia, no fuente única ni verdad absoluta.
- Si algo está **incompleto**, complétalo.
- Si algo está **mal o desactualizado**, corrígelo y dime explícitamente qué corregiste y por qué.
- Si falta un tema crítico que el entrevistador podría preguntar y no aparece en los documentos, agrégalo y márcalo como **[No estaba en los documentos]**.
- Si algo es incierto o depende del contexto, dilo en vez de inventar.

---

## REGLA 1 — Todo debe estar conectado, nada suelto

Esta es la prioridad número uno. Mi problema no es entender conceptos aislados: es entender **cómo se conectan entre sí**.

Cada concepto o tecnología que menciones debe indicar obligatoriamente:

| Campo | Qué debe decir |
|---|---|
| **Tipo** | Concepto / técnica / tecnología o producto / framework / estrategia / metodología / patrón arquitectónico |
| **Pertenece a** | De qué componente mayor forma parte (ej: embeddings pertenece a RAG; RAG pertenece a la capa de recuperación del agente) |
| **Paso del flujo** | Número del paso donde interviene (paso 3, paso 5...) |
| **Recibe de / entrega a** | Qué componente lo alimenta y a cuál alimenta |

Si un concepto **es realmente aislado** y no se conecta con el flujo principal, dilo explícitamente y explica por qué está aislado.

## REGLA 2 — Orden secuencial y jerárquico siempre

Numera todo en el orden real del ciclo de vida. Ejemplo del orden que espero: 1) ingesta de documentos → 2) chunking → 3) embeddings → 4) carga a base vectorial → 5) consulta del usuario → etc.

Nunca presentes conceptos en orden alfabético ni en lista plana sin jerarquía. El objetivo es que el entrevistador vea que entiendo el ciclo de vida completo.

## REGLA 3 — Alternativa vs. opcional (definiciones operativas)

Aplica esta distinción de forma estricta:

**ALTERNATIVA** = dos o más opciones **mutuamente excluyentes** que ocupan el mismo lugar del flujo. Eliges una u otra, no ambas.
> Ejemplos: AWS vs GCP vs Azure · LangGraph vs LangChain vs ADK · Pinecone vs pgvector vs OpenSearch · RAG vs fine-tuning (cuando compiten por el mismo objetivo).
>
> **Entregable:** (a) diagrama aparte para cada alternativa, (b) cuadro comparativo con criterio de decisión en una línea: *"elige X cuando..., elige Y cuando..."*.

**OPCIONAL** = componente que se puede agregar o quitar **sin romper el flujo principal**. Suma valor pero no es obligatorio.
> Ejemplos: re-ranking · caché semántico · human in the loop · guardrails de salida.
>
> **Entregable:** (a) incluirlo dentro del diagrama principal marcado como `(opcional)`, (b) agregarlo a la lista de conceptos, (c) indicar en una línea **cuándo se activa** y **cuándo no vale la pena**.

## REGLA 4 — Siglas y acrónimos

Cada sigla, acrónimo o abreviatura debe expandirse la primera vez que aparece, con su significado en español.
> Formato: **RAG** (*Retrieval-Augmented Generation* — generación aumentada por recuperación).

No asumas que entiendo nada. Mantén el término técnico en inglés (así lo va a decir el entrevistador) con la glosa en español al lado.

## REGLA 5 — Extensión

Voy a leer esto minutos antes de la entrevista. Sé puntual y concreto.

- Máximo **3 líneas** por concepto en la lista de conceptos.
- Máximo **2 frases** por celda en cuadros comparativos.
- Sin introducciones, sin resúmenes de lo que vas a hacer, sin cierres motivacionales.
- Prosa densa y directa, no relleno.

---

## ENTREGABLE

Entrega exactamente estas secciones, en este orden:

**1. Arquitectura de referencia (diagrama principal)**
Diagrama en Mermaid del flujo end-to-end, con pasos numerados y los componentes opcionales marcados `(opcional)`. Separa visualmente la fase *offline* (ingesta/indexación) de la fase *online* (consulta en tiempo real).

**2. Recorrido del flujo paso a paso**
Una línea por paso, numerada, en el orden del diagrama. Qué entra, qué pasa, qué sale.

**3. Lista de conceptos**
Ordenada según el flujo (no alfabética). Cada entrada con los 4 campos de la Regla 1 y la sigla expandida.

**4. Alternativas**
Diagramas aparte + cuadros comparativos, según la Regla 3.

**5. Los 4 temas donde el entrevistador profundizó**
Para cada uno: cómo se conecta con el flujo principal y en qué paso interviene.
- Datos personales (anonimización, pseudonimización, masking) — y en qué punto exacto del flujo se aplica cada uno.
- RAG vs fine-tuning: diferencias, cuándo combinarlos, cuándo no.
- Human in the loop: qué tipo de mecanismo es, dónde se inserta, cuándo sí y cuándo no.
- Seguridad: prompt injection, guardrails de entrada y de salida, parámetros del modelo (temperatura, top-p) y su efecto real.

**6. Guiones hablados**
Para las 6 preguntas más probables, una respuesta de **60–90 segundos** escrita como la diría en voz alta, empezando siempre por la estructura del flujo.

**7. Repreguntas probables**
Por cada guion, 2 repreguntas que me harían para profundizar, con respuesta de 2 líneas.

**8. Checklist de adaptación a otro caso**
5–7 preguntas que debo hacerme en vivo si me ponen un caso distinto, para mapearlo a esta misma arquitectura.

**9. Cómo responder lo que no sé**
Fórmula concreta para reconocer un límite sin perder credibilidad, con 2 ejemplos.

---

## FORMATO

- Responde en español.
- Diagramas en Mermaid.
- Usa tablas donde comparas, prosa donde explicas.
- Si el contenido no cabe en una respuesta, entrega las secciones 1 a 5 y pregúntame antes de continuar con el resto.
