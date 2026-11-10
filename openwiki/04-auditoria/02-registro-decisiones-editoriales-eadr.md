# REGISTRO DE DECISIÓN EDITORIAL Y ARQUITECTÓNICA (E-ADR)
## E-ADR-001: Desacoplamiento de Capas Canónicas y Preservación de la Entrega Monolítica

- **Artefacto Afectado:** `index.html`, `/data`, `/openwiki`, `/docs`
- **Criterio de la Policy en Tensión:** Criterio 7.1 (Zero-Build Archival) vs. Criterio 7.2 (Modularidad y Desacople de Capas de Datos)
- **Presencia de Drift Conceptual:** **NO** (Decisión Operativa y de Arquitectura Documental)
- **Estado:** **[APROBADO]**
- **Aprobador Autorizado:** Revisor General de Arquitectura y Gobernanza
- **Fecha de Decisión:** 2026-11-09

---

### 1. Contexto y Necesidad Epistémica
Históricamente, el proyecto `colombia-palma-desigualdad` nació como un único archivo `index.html` que albergaba simultáneamente la presentación visual, la interactividad de la curva SVG, el Waffle Chart y los arrays de datos `HISTORICAL_DATA` y `PALMA_DISTRIBUTION`.

Si bien este patrón garantizaba la portabilidad inmediata (*«doble clic en cualquier ordenador y funciona»*), generaba un acoplamiento indeseable:
1. Ningún agente o investigador podía consumir o validar las series estadísticas mediante APIs o herramientas de análisis de datos (Pandas, Polars, R) sin extraer manualmente los objetos de JavaScript incrustados en el HTML.
2. La ausencia de esquemas formales impedía validar la integridad matemática de los datos en pipelines de integración continua.
3. La fundamentación teórica de Gabriel Palma, las limitaciones de la GEIH y la relación con el debate filosófico de Isaiah Berlin quedaban atrapadas en la interfaz de usuario, sin una base de conocimiento navegable.

---

### 2. Decisión Adoptada
Se implementa una **Arquitectura de Doble Propósito (Dual-Layer Strategy)**:
1. **Capa Canónica Externa (`/data` y `/docs`):**
   - Los datos cuantitativos se formalizan como fuentes canónicas de verdad en `data/palma_colombia_series.json`, `data/palma_colombia_series.csv`, `data/palma_cookie_distribution.json` y `data/global_palma_comparison.json`.
   - Se crean esquemas formales JSON Schema Draft-07 en `data/schemas/` para validar la estructura de las series.
   - Todo el marco teórico, epistemológico y los contratos maestros se organizan en `docs/` y en la base interactiva `openwiki/` (Docsify).
2. **Capa de Presentación Autónoma (`index.html`):**
   - El artefacto `index.html` conserva su naturaleza monolítica *Zero-Build* (para que siga siendo 100% funcional sin servidor web ni compilación previa), pero sus constantes internas quedan declaradas como representaciones derivadas y sincronizadas de los datasets canónicos de `/data`.
   - Se inyectan en `index.html` los enlaces de navegación y metadatos hacia `openwiki/index.html` y los datos abiertos.

---

### 3. Consecuencias y Trade-offs Asumidos
* **Beneficio Cognitivo y Técnico:** Máxima modularidad, trazabilidad y auditabilidad para agentes de IA y científicos de datos, sin sacrificar la resiliencia y simplicidad de la visualización web.
* **Costo / Trade-off:** Exige un contrato de sincronización (`CON-DAT-001` y `CON-TEC-001`) para garantizar que cualquier actualización en los microdatos del DANE se refleje concurrentemente en `/data` y en las constantes de `index.html`.
