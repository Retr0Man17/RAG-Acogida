# Documentación del levantamiento de requerimientos — Asistente RAG Familias de Acogida

Carpeta para los equipos de NLP / vectorización, IU/UX y desarrollo. El documento de requerimientos define *qué* debe hacer el sistema; las guías ayudan a cada equipo a *construirlo*.

| Archivo | Para quién | Contenido |
| --- | --- | --- |
| `00_documento_requerimientos.md` | Todos | Documento formal completo: visión, personas, acceso y roles, 54 historias con criterios Gherkin, requerimientos no funcionales y de privacidad, corpus, supuestos y riesgos |
| `01_hoja_de_ruta_tecnica.md` | Todos los equipos técnicos | Orden de construcción por capas, para que lo construido siempre funcione |
| `02_contrato_nlp_taxonomia_metadatos.md` | NLP / vectorización y desarrollo | Taxonomía, metadatos, esquema SQL, formato de fragmentos y contrato de recuperación |
| `03_golden_set_evaluacion.md` + `golden_set.csv` | NLP y desarrollo | 51 preguntas para medir recuperación, derivación y honestidad |
| `04_guia_ui_ux.md` | IU/UX y frontend | Pantallas, flujos, componentes, estados y textos de ejemplo |
| `diagramas/` | Todos | Modelo de acceso, arquitectura funcional, flujo del semáforo y mapa de historias (PNG) |

Los identificadores (HU-xx, RNF-xx, PRI-xx, COR-xx, S-xx) remiten al documento de requerimientos. Los diagramas de las guías usan Mermaid, que GitHub muestra directamente.

La versión editable y vigente del documento de requerimientos está en Claude Docs; esta copia en Markdown corresponde al 2 de noviembre de 2026.
