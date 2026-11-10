# CONTRATO MAESTRO DE GOBERNANZA DE DATOS Y PROCEDENCIA
## Código Normativo: CON-DAT-001 | Versión: 1.0.0 | Estado: [VIGENTE]
### Repositorio: colombia-palma-desigualdad (Paso 5)

> [!IMPORTANT]
> **Estatus Canónico:** Este contrato rige la captura, estructuración, validación, actualización y auditoría de todas las series cuantitativas y microdatos empíricos del repositorio. Es de cumplimiento obligatorio para autores humanos, ingenieros de datos y agentes autónomos de IA.

---

## 1. Propósito y Alcance

### 1.1. Propósito
Garantizar la integridad matemática, la trazabilidad de fuentes y la reproducibilidad absoluta de todas las cifras sobre el Coeficiente de Palma, distribución decílica y comparaciones internacionales utilizadas en el sitio web y en la documentación técnica.

### 1.2. Alcance
Aplica a todos los archivos dentro del directorio `/data` (`palma_colombia_series.json`, `palma_colombia_series.csv`, `palma_cookie_distribution.json`, `global_palma_comparison.json`), a sus esquemas de validación en `/data/schemas/` y al registro de procedencia `data/provenance.md`, así como a los objetos de datos consumidos en tiempo de ejecución por `index.html`.

---

## 2. Principios y Reglas Obligatorias

1. **Principio de Trazabilidad Primaria [VIGENTE]:** Ninguna cifra estadística puede incorporarse al repositorio sin un vínculo documental verificable a una fuente primaria oficial (DANE, Banco Mundial, CEPAL, OCDE).
2. **Principio de Formato Abierto Dual [VIGENTE]:** Todo dataset canónico de series temporales debe residir simultáneamente en formato JSON estructurado y CSV tabular, garantizando interoperabilidad para agentes y analistas.
3. **Principio de Validación Estricta por Esquema [VIGENTE]:** Todo archivo JSON de datos debe validar satisfactoriamente contra su respectivo JSON Schema Draft-07 sin errores de tipo ni claves no declaradas.
4. **Regla de Invarianza de las 100 Galletas [VIGENTE]:** En cualquier dataset o modelo de distribución porcentual, la suma acumulada de los deciles debe ser idéntica a 100 ($\sum \text{share} \equiv 100\%$). Queda prohibido el truncamiento que produzca sumas distorsionadas (ej. 99% o 101%).
5. **Regla de No-Interpolación Artificial [VIGENTE]:** En series temporales históricas con vacíos de encuesta (ej. años no cubiertos por el DANE), queda prohibido inventar datos interpolados sin declarar explícitamente en metadatos que se trata de una estimación econométrica.

---

## 3. Responsabilidades y Límites de Actuación

### 3.1. Atribuciones del Agente
- Validar esquemas JSON y reportar discrepancias.
- Actualizar series históricas cuando el DANE publique comunicados oficiales de Pobreza Monetaria, siempre que se incorpore la cita oficial y se mantenga la coherencia del esquema.
- Extraer o regenerar archivos `.csv` a partir de fuentes canónicas `.json`.

### 3.2. Límites y Prohibiciones
- **PROHIBIDO:** Modificar retroactivamente cifras históricas de años cerrados sin justificación documental de una reponderación oficial del marco censal del DANE (ej. empalme MESEP).
- **PROHIBIDO:** Alterar la definición matemática del Coeficiente de Palma ($D_{10} / \sum_{1}^{4} D_i$).

---

## 4. Criterios Verificables de Cumplimiento

| ID Criterio | Descripción del Criterio | Prueba Observable |
| :--- | :--- | :--- |
| **C-DAT-01** | Conformidad de esquema JSON | Ejecución de validador de esquemas contra `data/schemas/*.json` arrojando 0 errores. |
| **C-DAT-02** | Paridad JSON / CSV | Coincidencia exacta de filas y valores entre `.json` y `.csv`. |
| **C-DAT-03** | Suma exacta del 100% | `poorShare + middleShare + richShare === 100` verificado en código y tests. |
| **C-DAT-04** | Metadatos completos | Presencia de fuente, año, institución, cobertura y licencia en el bloque de metadatos. |

---

## 5. Procedimientos de Validación

1. **Validación Automática en CI/CD:**  
   Un script de validación inspecciona que los archivos en `/data` cumplan los esquemas JSON y que los valores numéricos coincidan con las constantes de `index.html`.
2. **Validación Manual de Procedencia:**  
   Ante una actualización anual, el revisor debe contrastar la cifra propuesta contra el Boletín Técnico de Pobreza Monetaria emitido por el DANE.

---

## 6. Gestión de Desviaciones y Excepciones (E-ADR)

Cualquier desviación (por ejemplo, el uso de una estimación preliminar ante retrasos en la publicación del DANE) debe documentarse mediante un **Registro de Decisión Editorial (E-ADR)** bajo la tipología *Excepción Epistémica*, requiriendo la firma del Custodio Conceptual.

---

## 7. Relación con Otros Contratos

- **Subordinado a:** `POL-ED-001` (Policy Editorial Maestra) en lo relativo a integridad de afirmaciones empíricas (Vector 2).
- **Coordina con:** `CON-EPI-001` (Gobernanza Epistemológica) para el desacople fáctico-interpretativo.
- **Alimenta a:** `CON-VIZ-001` (Gobernanza Visual) para el trazado exacto sin *Lie Factor*.

---

## 8. Versionado y Mantenimiento

- **Versión 1.0.0 (2026-11-09):** Emisión canónica inicial e incorporación a la arquitectura OpenWiki.
- **Frecuencia de Mantenimiento:** Anual, coincidiendo con la divulgación anual de pobreza monetaria del DANE (típicamente entre mayo y julio de cada año).
