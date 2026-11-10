# CONTRATO MAESTRO DE GOBERNANZA VISUAL, ISOMORFISMO SEMÁNTICO Y A11Y
## Código Normativo: CON-VIZ-001 | Versión: 1.0.0 | Estado: [VIGENTE]
### Repositorio: colombia-palma-desigualdad (Paso 5)

> [!IMPORTANT]
> **Estatus Canónico:** Este contrato rige la fidelidad matemática de las representaciones visuales, la erradicación del «ruido visual» (*chartjunk*), el cumplimiento estricto de accesibilidad perceptual (WCAG 2.1 AA) y la ergonomía responsiva para múltiples dispositivos.

---

## 1. Propósito y Alcance

### 1.1. Propósito
Garantizar que todo elemento gráfico, diagrama vectorial, gráfico estadístico y animación interactiva cumpla una función cognitiva precisa, represente con exactitud isomórfica los datos subyacentes y sea plenamente perceptible y operable por cualquier usuario, independientemente de sus capacidades físicas o del dispositivo utilizado.

### 1.2. Alcance
Aplica a los componentes SVG embebidos, Waffle Chart interactivo, gráficos Tufte Range-Frame, selectores de idioma, tokens CSS de color, escala tipográfica fluida y diseño responsivo móvil/escritorio en `index.html`.

---

## 2. Principios y Reglas Obligatorias

1. **Principio de Isomorfismo Semántico-Visual [VIGENTE]:** Todo gráfico debe mapear fielmente relaciones cuantitativas o lógicas. Quedan proscritos los gráficos puramente ornamentales que simulen datos falsos o que utilicen escalas distorsionadas (*Lie Factor $\ne 1.0$*).
2. **Principio de Accesibilidad Perceptual WCAG 2.1 AA [VIGENTE]:**
   - La relación de contraste cromático entre texto y fondo debe ser igual o superior a **4.5:1** para texto normal y **3.0:1** para texto grande ($\ge 18\text{pt}$ o $\ge 14\text{pt}$ en negrita) y componentes de interfaz.
   - Todo elemento interactivo debe incluir un anillo de enfoque de alto contraste (`outline: 3px solid #005A9C; outline-offset: 3px;`).
3. **Regla de Tamaño Táctil Mínimo (*Touch Target*) [VIGENTE]:** En pantallas táctiles y dispositivos móviles, ningún botón, galleta interactiva, control de idioma o enlace puede tener un área interactiva efectiva menor a **$44 \times 44\text{ px}$**.
4. **Regla de Cero Desbordamiento Horizontal (*No Horizontal Scroll*) [VIGENTE]:** En cualquier ancho de ventana comprendido entre 320 px y 2560 px, debe verificarse estrictamente que $\text{scrollWidth} \equiv \text{clientWidth}$. Queda terminantemente prohibido el scroll horizontal involuntario.
5. **Regla de Prevención de Colisión de Etiquetas [VIGENTE]:** En el trazador SVG de series históricas, las cajas tipográficas de anotaciones para años contiguos o puntos de inflexión deben calcular dinámicamente sus desplazamientos espaciales para evitar la superposición de textos.

---

## 3. Responsabilidades y Límites de Actuación

### 3.1. Atribuciones del Agente
- Optimizar el marcado SVG y las clases CSS para garantizar contraste WCAG.
- Ajustar márgenes, padding y `viewBox` para eliminar desbordamientos horizontales.
- Añadir atributos `aria-label`, `aria-hidden` y regiones `sr-only` para tecnologías de asistencia.
- Refinar la escala tipográfica en `clamp()` para preservar la jerarquía visual en resoluciones intermedias (tablets y pantallas plegables).

### 3.2. Límites y Prohibiciones
- **PROHIBIDO:** Cambiar la paleta canónica editorial Tufte por colores estridentes no contrastados.
- **PROHIBIDO:** Introducir bibliotecas pesadas de gráficos (D3, Chart.js, Highcharts) que rompan la filosofía *Zero-Build*.
- **PROHIBIDO:** Ocultar información estadística en pantallas móviles con el pretexto de ahorrar espacio.

---

## 4. Criterios Verificables de Cumplimiento

| ID Criterio | Descripción del Criterio | Prueba Observable |
| :--- | :--- | :--- |
| **C-VIZ-01** | Ratio de Contraste WCAG 2.1 AA | Evaluación automatizada con `axe-core` arrojando 0 violaciones de contraste. |
| **C-VIZ-02** | Touch Targets $\ge 44 \times 44\text{ px}$ | Dimensiones del bounding box de botones evaluadas en viewport de 360 px. |
| **C-VIZ-03** | Cero scroll horizontal | `document.documentElement.scrollWidth === window.innerWidth` en 320, 375, 768 y 1080 px. |
| **C-VIZ-04** | Cero colisión de texto | Comprobación de no superposición de etiquetas SVG en puntos 2018, 2019 y 2020. |

---

## 5. Procedimientos de Validación

1. **Auditoría Automatizada de Accesibilidad:** Inspección con herramientas de auditoría visual (axe / htmlhint / lighthouse).
2. **Prueba Multi-Viewport:** Comprobación del renderizado en breakpoints: 320 px (móvil estrecho), 375 px (iPhone clásico), 768 px (tablet vertical), 1080 px (desktop base) y 1440 px (pantalla ancha).

---

## 6. Gestión de Desviaciones y Excepciones (E-ADR)

Cualquier excepción (por ejemplo, el uso de un elemento decorativo sutil en una textura de fondo que no requiera texto alternativo) debe clasificarse con `aria-hidden="true"` y documentarse en un **E-ADR Operativo**.

---

## 7. Relación con Otros Contratos

- **Subordinado a:** `POL-ED-001` (Vector 5: Comunicación Visual e Isomorfismo Semántico).
- **Recibe de:** `CON-DAT-001` las coordenadas numéricas a proyectar en los lienzos.

---

## 8. Versionado y Mantenimiento

- **Versión 1.0.0 (2026-11-09):** Formalización canónica inicial en OpenWiki.
- **Mantenimiento:** Por cada modificación de layout, paleta o lógica SVG.
