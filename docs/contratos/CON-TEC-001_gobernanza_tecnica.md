# CONTRATO MAESTRO DE GOBERNANZA TÉCNICA, ARQUITECTURA Y PUBLICACIÓN
## Código Normativo: CON-TEC-001 | Versión: 1.0.0 | Estado: [VIGENTE]
### Repositorio: colombia-palma-desigualdad (Paso 5)

> [!IMPORTANT]
> **Estatus Canónico:** Este contrato rige la arquitectura de software, la filosofía de despliegue, la preservación a largo plazo, la gestión de dependencias y la automatización CI/CD del repositorio. Es la salvaguarda contra la deuda técnica y la obsolescencia de herramientas.

---

## 1. Propósito y Alcance

### 1.1. Propósito
Garantizar que el artefacto sea perpetuamente reproducible, auto-suficiente y ejecutable en cualquier navegador web moderno sin requerir procesos de compilación en tiempo de ejecución, asegurando una vida útil mínima de 30 años sin degradación funcional.

### 1.2. Alcance
Aplica a la arquitectura de archivos del repositorio, la estructura monolítica de `index.html`, la integración con GitHub Pages, el workflow `.github/workflows/deploy.yml` y la separación de capas canónicas.

---

## 2. Principios y Reglas Obligatorias

1. **Invariante Zero-Build [VIGENTE]:** Prohibido incorporar dependencias de compilación o bundlers (Vite, Webpack, Babel, Parcel) en tiempo de ejecución para el sitio web principal. El código fuente ES el código de producción.
2. **Principio de Rutas Relativas Universales [VIGENTE]:** Todos los enlaces internos, importaciones de estilos, scripts o recursos locales deben utilizar rutas relativas (`./styles.css`, `openwiki/index.html`, `../data/`), sin barras inclinadas iniciales absolutas (`/`) que rompan el enrutamiento bajo subdirectorios de GitHub Pages (`/colombia-palma-desigualdad/`).
3. **Principio de Despliegue Automatizado y Determinístico [VIGENTE]:** Todo push o merge a la rama `main` debe desencadenar automáticamente el workflow de GitHub Actions que audita el marcado HTML con `htmlhint` antes de promover a producción.
4. **Regla de Inviolabilidad del Historial Git [VIGENTE]:** El historial público del repositorio debe reflejar exclusivamente commits limpios bajo el estándar de Conventional Commits (`feat:`, `fix:`, `docs:`, `style:`, `refactor:`, `test:`, `chore:`). Queda terminantemente prohibido introducir o conservar referencias a herramientas o extensiones efímeras (`.gitclaude`).
5. **Regla de Auto-Contención Archival-Safe [VIGENTE]:** El archivo `index.html` debe poder ejecutarse desconectado de la red local (offline), conservando toda su lógica interactiva, cálculos aritméticos y visualizaciones SVG nativas.

---

## 3. Responsabilidades y Límites de Actuación

### 3.1. Atribuciones del Agente
- Validar sintaxis HTML5 y ejecutar linters locales (`htmlhint`).
- Optimizar el pipeline de GitHub Actions en `.github/workflows/deploy.yml`.
- Auditar y corregir enlaces rotos o rutas relativas incorrectas.
- Mantener la coherencia entre `data/`, `openwiki/` y `index.html`.

### 3.2. Límites y Prohibiciones
- **PROHIBIDO:** Ejecutar `git push --force` sobre ramas protegidas o remotas sin autorización explícita.
- **PROHIBIDO:** Instalar frameworks pesados (React, Vue, Angular, Svelte) que destruyan la naturaleza *Zero-Build*.

---

## 4. Criterios Verificables de Cumplimiento

| ID Criterio | Descripción del Criterio | Prueba Observable |
| :--- | :--- | :--- |
| **C-TEC-01** | Cero Build en Runtime | `index.html` se abre directamente con protocolo `file:///` y funciona al 100%. |
| **C-TEC-02** | Validación HTML5 limpia | `htmlhint index.html` arrojando 0 errores y 0 advertencias. |
| **C-TEC-03** | Rutas relativas | Cero URLs que comiencen con `/` absoluto en atributos `href` o `src`. |
| **C-TEC-04** | Historial Git higiénico | Cero ocurrencias de `.gitclaude` en commits, diffs o árboles de git. |

---

## 5. Procedimientos de Validación

1. **Validación Pre-Commit:** Verificación de sintaxis HTML y comprobación de integridad de enlaces internos.
2. **Validación CI/CD:** Ejecución de GitHub Actions con Node 20 y `htmlhint`.

---

## 6. Gestión de Desviaciones y Excepciones (E-ADR)

Cualquier excepción técnica (por ejemplo, el uso transitorio de un CDN externo para fuentes tipográficas) debe documentarse en un **E-ADR Técnico/Operativo**.

---

## 7. Relación con Otros Contratos

- **Subordinado a:** `POL-ED-001` (Vector 7: Durabilidad, Modularidad y Prevención de Obsolescencia).
- **Provee la plataforma técnica para:** `CON-DAT-001`, `CON-EDT-001` y `CON-VIZ-001`.

---

## 8. Versionado y Mantenimiento

- **Versión 1.0.0 (2026-11-09):** Formalización canónica inicial en OpenWiki.
- **Mantenimiento:** Por cada modificación de workflows de despliegue o arquitectura de hosting.
