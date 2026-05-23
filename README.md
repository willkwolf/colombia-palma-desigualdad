# La Galleta Colombiana — Radiografía de la Desigualdad

Visualización interactiva y análisis crítico sobre la concentración de ingresos en Colombia a través del **Índice de Palma** (2002–2023).

Este proyecto ofrece una lectura honesta y accesible del Índice de Palma, contrastando la teoría con la analogía tangible de "repartir 100 galletas entre 10 personas" y contextualizando los datos oficiales del DANE (GEIH-MESEP) con fuentes secundarias del Banco de la República, la CEPAL y WID.world.

---

## 🔬 Contexto Analítico: ¿Por qué el Índice de Palma?

El economista Gabriel Palma (Universidad de Cambridge) observó una constante incómoda: en casi todo el mundo, la clase media (el 50% de la población entre los deciles 5 y 9) captura de forma sumamente estable **entre el 45% y el 55%** del ingreso nacional. Es el "ruido estable" del sistema de distribución.

La desigualdad real ocurre en las colas (los extremos):
$$\text{Índice de Palma} = \frac{\text{Ingreso total del 10\% más rico (Decil 10)}}{\text{Ingreso total del 40\% más pobre (Deciles 1, 2, 3 y 4)}}$$

Un Palma de **1.0** representa una igualdad perfecta entre los extremos (el decil superior gana en conjunto lo mismo que el 40% inferior). Colombia ha oscilado históricamente entre **3.7 y 5.0** en los últimos 20 años, situándose como uno de los países más desiguales de América Latina y del mundo.

---

## 🛠️ Decisiones de Arquitectura Defensiva (Para los Próximos Años)

Este proyecto ha sido desarrollado siguiendo una **filosofía de diseño defensivo y de archivo (archival-safe)**:

### 1. Formato Monolítico Cero-Dependencias
* **Decisión**: La aplicación se compone de un archivo estructurado único: `index.html` (el cual incluye sus propios estilos CSS y la lógica en Javascript).
* **Razón**: En el ecosistema moderno del desarrollo web, los frameworks (React, Next.js, Svelte), compiladores (Vite, Webpack) y dependencias auxiliares de NPM sufren obsolescencia rápida. Un proyecto compilado con Node.js en 2026 muy probablemente no compilará en 2035 debido a incompatibilidades de versiones.
* **Durabilidad**: Este archivo no tiene ningún paso de compilación ni dependencias externas vulnerables. Puede abrirse directamente desde el disco local haciendo doble clic en cualquier navegador web moderno de los próximos 20 o 30 años y **funcionará exactamente igual**.

### 2. Próxima Release: Automatización y Kaizen
* **Visión de Auto-mantenibilidad**: Para la próxima versión, mejoraremos la arquitectura separando la presentación de los datos. Crearemos un archivo de datos estructurado (`data.json`) y un parser ligero en JS que lo consuma. Esto permitirá actualizar las cifras de forma automatizada mediante integraciones con el API de Datos Abiertos del DANE o scripts automáticos de raspado, sin comprometer la inmunidad a la obsolescencia que tiene el núcleo estático actual.

---

## 📊 Contexto del Dato y Puntos Ciegos

Para analizar la infografía sin estirar el indicador más allá de sus límites metodológicos, es crucial entender de qué está hecha "la galleta" (el ingreso):

* **Qué SÍ mide**: El Palma de esta infografía utiliza el **ingreso monetario disponible del hogar, post-transferencias monetarias**, reportado en la Gran Encuesta Integrada de Hogares (GEIH) del DANE (serie MESEP empalmada). Incluye salarios, honorarios, pensiones, arriendos imputados y transferencias institucionales (subsidios de Familias en Acción, etc.).
* **Puntos Ciegos (Lo que NO mide)**:
  * **Riqueza y Patrimonio**: Mide flujos de ingresos anuales, no stock de riqueza (propiedad de tierras, acciones o inmuebles). La desigualdad de riqueza en Colombia es considerablemente superior (3 a 4 veces mayor).
  * **Subreporte del Decil Superior**: Las encuestas de hogares sufren de un severo subreporte de ingresos de capital y dividendos en el 1% y 0.1% más rico. Los multimillonarios reales son invisibles en las encuestas, por lo que el Palma real es mayor que el reportado.
  * **Brechas Regionales**: El Palma nacional de **3.7** suaviza realidades brutales. Zonas rurales o departamentos rezagados como Chocó registran índices de pobreza extrema y desigualdad locales que duplican la media nacional (ej. Quibdó con 60.1% de pobreza monetaria en 2023).

---

## 🔧 Guía de Mantenimiento (Edición de Datos)

Para actualizar los datos de la serie histórica y el simulador cuando se publiquen nuevas encuestas del DANE, sigue estas instrucciones:

El gráfico histórico SVG y el waffle chart de la analogía de las galletas se renderizan **dinámicamente desde un bloque de configuración de JavaScript** en el propio `index.html`. No requieres editar coordenadas de trazado SVG manualmente.

### Paso 1: Localizar los datos de la serie
Abre `index.html` en un editor de texto y busca el bloque `<script>` que contiene los datos del gráfico:

```javascript
const HISTORICAL_DATA = [
  { year: 2002, value: 4.9, phase: 'crisis' },
  { year: 2004, value: 4.7, phase: 'crisis' },
  ...
  { year: 2023, value: 3.7, phase: 'recuperacion' }
];
```

### Paso 2: Agregar o modificar un registro
Simplemente agrega un nuevo objeto al array. Las categorías de `phase` disponibles son:
* `'crisis'`: Alto riesgo / Palma > 4.5 (Color óxido/rojo).
* `'mejora'`: Descenso gradual (Color arcilla/ámbar).
* `'regresion'`: Impacto COVID (Color pizarra/gris).
* `'recuperacion'`: Periodo reciente (Color bosque/verde).

El motor del gráfico recalculará de forma automática las coordenadas del eje SVG de Tufte (Range-Frame) basándose en los valores máximos y mínimos del array, dibujando la línea perfectamente adaptada sin necesidad de recalcular pixeles a mano.

### Paso 3: Modificar las galletas de la analogía
Para actualizar las proporciones del waffle chart (las 100 galletas), localiza el objeto de distribución:

```javascript
const PALMA_DISTRIBUTION = {
  poorShare: 12,    // % de ingreso capturado por el 40% pobre
  middleShare: 43,  // % de ingreso capturado por el 50% medio
  richShare: 45     // % de ingreso capturado por el 10% rico
};
```
*Asegúrate de que la suma sea exactamente 100*. Al guardar el archivo, la cuadrícula de 100 celdas SVG se re-coloreará automáticamente reflejando la nueva distribución e ingresos por persona con precisión matemática y sin Lie Factor.

---

## 🤖 Pipeline de GitHub Actions (.github/workflows/deploy.yml)

El proyecto cuenta con un flujo de trabajo integrado en GitHub Actions que se ejecuta en cada push a la rama `main`:
1. **Validación de HTML5 y CSS**: Comprobación estática para evitar etiquetas mal cerradas o estilos inválidos.
2. **Escaneo Automático de Accesibilidad**: Utiliza `@axe-core/cli` mediante un runner de Node.js para certificar que no se introducen violaciones WCAG 2.1 AA (errores de contraste, falta de ARIA).
3. **Despliegue a GitHub Pages**: Si los tests son exitosos, el pipeline despliega la versión actualizada de forma inmediata en el hosting estático público del repositorio.
