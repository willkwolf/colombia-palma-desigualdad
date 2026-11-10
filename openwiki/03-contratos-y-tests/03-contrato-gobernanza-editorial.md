# CONTRATO MAESTRO DE GOBERNANZA EDITORIAL, NARRATIVA Y PARIDAD LINGÜÍSTICA
## Código Normativo: CON-EDT-001 | Versión: 1.0.0 | Estado: [VIGENTE]
### Repositorio: colombia-palma-desigualdad (Paso 5)

> [!IMPORTANT]
> **Estatus Canónico:** Este contrato rige la estructura narrativa, la calidad textual, la consistencia terminológica, los estándares de citación académica y la paridad lingüística bilingüe estricta (Español / Inglés) en todo el ecosistema documental e interactivo.

---

## 1. Propósito y Alcance

### 1.1. Propósito
Asegurar una experiencia de lectura fluida, elegante, académica y accesible, manteniendo la dignidad del formato editorial clásico de museo y garantizando que los lectores internacionales cuenten con una versión en inglés de idéntica profundidad conceptual que la versión en español.

### 1.2. Alcance
Aplica a la interfaz interactiva `index.html`, los diccionarios de internacionalización (`I18N`), el `README.md` del repositorio, y toda la documentación en `openwiki/` y `/docs`.

---

## 2. Principios y Reglas Obligatorias

1. **Principio de Paridad Lingüística Estricta 1:1 [VIGENTE]:** Ninguna sección, párrafo explicativo, etiqueta gráfica o nota histórica puede publicarse en español sin su contraparte exacta en inglés. Queda prohibida la traducción automática descuidada que altere términos económicos precisos.
2. **Principio de Densidad Semántica y Cero Relleno [VIGENTE]:** La prosa debe ser sobria, precisa y con alta densidad conceptual. Quedan proscritos los lugares comunes, la verborrea burocrática, los adjetivos vacíos y la retórica inflamatoria.
3. **Principio de Citación Canónica Universal [VIGENTE]:** Todo artefacto debe ofrecer en su pie y documentación su bloque de citación formal tanto en formato **APA 7ma Edición** como en bloque **BibTeX** perfectamente tipado.
4. **Regla de Consistencia Terminológica [VIGENTE]:** Los términos técnicos deben utilizarse de forma unívoca a lo largo de todos los documentos:
   - Utilizar *«Coeficiente de Palma»* o *«Ratio de Palma»* (no inventar *«Índice de Galletas»* como término técnico, sino mantenerlo como metáfora pedagógica).
   - Utilizar *«Ingreso disponible per cápita de la unidad de gasto»* para la variable DANE.
   - Distinguir taxativamente entre *«pobreza monetaria»*, *«pobreza multidimensional (IPM)»* y *«desigualdad de ingresos»*.
5. **Regla de Estructura de Museo Técnico [VIGENTE]:** El pie de página del artefacto debe presentarse como una *Placa de Museo Técnica*, declarando autoría (William Camilo Artunduaga Viana), ubicación (Cali, Colombia), año de referencia, licencia abierta (CC BY 4.0) y la navegación hacia el ecosistema.

---

## 3. Responsabilidades y Límites de Actuación

### 3.1. Atribuciones del Agente
- Corregir errores ortográficos, tipográficos y de puntuación.
- Asegurar la simetría de claves en el diccionario `I18N`.
- Formatear referencias bibliográficas según APA 7 y BibTeX.
- Mejorar la fluidez sintáctica en ambos idiomas sin cambiar el sentido.

### 3.2. Límites y Prohibiciones
- **PROHIBIDO:** Eliminar contenido sustantivo o explicaciones metodológicas con el pretexto de «resumir».
- **PROHIBIDO:** Alterar la voz autoral serena, reflexiva e incisiva del proyecto.

---

## 4. Criterios Verificables de Cumplimiento

| ID Criterio | Descripción del Criterio | Prueba Observable |
| :--- | :--- | :--- |
| **C-EDT-01** | Simetría bilingüe total | Verificación de que cada clave `_es` posee su clave `_en` correspondiente en código y datos. |
| **C-EDT-02** | Citación formal | Presencia de citas APA 7 y BibTeX válidas en `index.html`, `README.md` y `openwiki/`. |
| **C-EDT-03** | Ortografía y gramática impecable | Cero errores ortográficos detectables en español e inglés. |
| **C-EDT-04** | Formato de metadatos | Cabeceras estructuradas de metadatos en todos los capítulos de la OpenWiki. |

---

## 5. Procedimientos de Validación

1. **Test de Integridad Lingüística:** Comparación automatizada de llaves en el objeto `I18N`.
2. **Revisión de Estilo:** Cotejo contra el Vector 4 de la Policy POL-ED-001.

---

## 6. Gestión de Desviaciones y Excepciones (E-ADR)

Cualquier asimetría deliberada (por ejemplo, mantener una cita histórica en su idioma original con glosa al pie) debe registrarse mediante un **E-ADR Operativo**.

---

## 7. Relación con Otros Contratos

- **Subordinado a:** `POL-ED-001` (Vectores 4 y 6).
- **Coordina con:** `CON-VIZ-001` para la adaptación tipográfica y espacial de textos bilingües.

---

## 8. Versionado y Mantenimiento

- **Versión 1.0.0 (2026-11-09):** Formalización canónica inicial en OpenWiki.
- **Mantenimiento:** Continuo con cada adición o revisión de contenido.
