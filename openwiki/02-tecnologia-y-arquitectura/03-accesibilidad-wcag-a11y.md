# 03. Accesibilidad Universal (WCAG 2.1 Nivel AA) y Usabilidad Inclusiva

> **Metadatos Canónicos:**  
> - **Dominio:** Dominio II — Tecnología, Arquitectura e Isomorfismo Visual  
> - **Propósito:** Especificar los criterios de accesibilidad perceptual, cognitiva y motriz implementados en el artefacto según la norma internacional W3C WCAG 2.1 AA.  
> - **Audiencia:** Desarrolladores frontend, auditores de accesibilidad (a11y), diseñadores UX y evaluadores automatizados.  
> - **Alcance:** Marcado ARIA, gestión de teclado, contraste cromático, lectores de pantalla y soporte táctil móvil.  
> - **Criterio Normativo:** Cumplimiento 100% de WCAG 2.1 AA ([VIGENTE] en CON-VIZ-001 y POL-ED-001).

---

## 1. Compromiso Ético con la Accesibilidad

En un proyecto centrado en la justicia distributiva y la reducción de brechas sociales, la exclusión digital sería una contradicción ética intolerable. *La Galleta Colombiana* está concebida para ser plenamente operable por personas ciegas, con baja visión, con discapacidades motrices o usuarias exclusivas de teclado.

---

## 2. Implementación de los Cuatro Principios WCAG 2.1

### 2.1. Principio 1: Perceptible
- **Contraste de Color Riguroso:** Toda combinación de texto y fondo supera con creces el ratio mínimo de $4.5:1$ para texto normal y $3.0:1$ para texto de gran tamaño o elementos de interfaz gráfica (verificación en `02-sistema-visual-tufte.md`).
- **Alternativas Textuales:** Gráficos SVG interactivos y Waffle Charts cuentan con resúmenes textuales accesibles (`sr-only`) que explican los valores numéricos antes del renderizado visual.
- **Jerarquía Tipográfica:** Uso de `rem` y `clamp()` para permitir que los usuarios amplíen la escala de fuentes de su navegador hasta un 200% sin truncamientos ni roturas de layout.

### 2.2. Principio 2: Operable
- **Navegabilidad 100% por Teclado:**
  - Enlace de salto inicial (*Skip Link*) accesible mediante `Tab`: *«Saltar al contenido principal»*.
  - Indicador de foco visible (`outline: 3px solid #005A9C; outline-offset: 3px;`) en todos los enlaces, botones y elementos del Waffle Chart.
  - Cero trampas de foco (*No keyboard traps*).
- **Objetivos Táctiles Móviles (*Touch Targets*):**  
  Todos los botones interactivos (selector de idioma, puntos de la curva, botones de galleta) poseen áreas efectivas de toque superiores a los $44 \times 44\text{ px}$ requeridos por la norma WCAG 2.5.5.

### 2.3. Principio 3: Comprensible
- **Atributos de Idioma Explícitos:** Elemento raíz con `lang="es"`, actualizado reactivamente a `lang="en"` cuando el usuario conmuta el idioma.
- **Predictibilidad:** Ningún cambio de contexto o salto inesperado al recibir el foco.

### 2.4. Principio 4: Robusto
- **Semántica HTML5 Pura:** Uso de `<header>`, `<main>`, `<section>`, `<nav>`, `<footer>`, `<figure>`, `<figcaption>` y encabezados ordenados jerárquicamente (`<h1>` a `<h3>`).
- **Compatibilidad con Tecnologías de Asistencia:** Validación automatizada con `htmlhint` y compatibilidad certificada con NVDA, JAWS y VoiceOver.
