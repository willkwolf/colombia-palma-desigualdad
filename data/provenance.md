# REGISTRO DE PROCEDENCIA Y METADATOS DE DATOS (PROVENANCE)
## Repositorio: colombia-palma-desigualdad (Paso 5)
**Código:** PROV-DAT-001  
**Versión:** 1.0.0  
**Fecha:** 2026-11-09  
**Estado:** [CANÓNICO]

---

## 1. Fuentes Primarias Oficiales

Los datos empleados en este repositorio proceden de fuentes estadísticas oficiales de Colombia y organismos multilaterales:

1. **Departamento Administrativo Nacional de Estadística (DANE) — Colombia:**
   - **Encuesta Base:** Gran Encuesta Integrada de Hogares (GEIH).
   - **Serie Empalmada:** Misión para el Empalme de las Series de Empleo, Pobreza y Desigualdad (MESEP) 2002–2010 y GEIH continua (Marcos 2005 y 2018).
   - **Variable Canónica:** Ingreso disponible per cápita de la unidad de gasto (post-transferencias gubernamentales en dinero, subsidios directos como Familias en Acción/Renta Ciudadana, arriendo imputado, pensiones y salarios líquidos).
   - **Publicación de Referencia:** DANE (2024). *Pobreza Monetaria y Desigualdad en Colombia — Resultados 2023*. Boletín Técnico Nacional.

2. **Organismos Multilaterales (Comparativa Global):**
   - **Banco Mundial:** *World Development Indicators (WDI)* — Serie histórica de Palma Ratio por país.
   - **CEPAL:** *Panorama Social de América Latina* — Informes anuales de distribución decílica del ingreso en el Cono Sur y la región Andina.
   - **OCDE:** *OECD Income Distribution Database (IDD)* — Indicadores de desigualdad para Europa Occidental, Nórdicos y Norteamérica.

---

## 2. Definición Operativa del Coeficiente de Palma

Formulado por el economista chileno **José Gabriel Palma** (Universidad de Cambridge, 2011):

$$\text{Coeficiente de Palma} = \frac{D_{10}}{\sum_{i=1}^{4} D_i}$$

Donde:
- $D_{10}$: Proporción de la masa de ingresos capturada por el decil 10 (el 10% más rico de la población).
- $\sum_{i=1}^{4} D_i$: Proporción de la masa de ingresos acumulada por los deciles 1, 2, 3 y 4 (el 40% más pobre de la población).

### Hipótesis Empírica Subyacente (El 50% Medio):
Palma observó a través de decenas de países que los deciles 5 al 9 capturan de manera sumamente estable aproximadamente la mitad del ingreso nacional ($\approx 50\% \pm 5\%$). Por ende, la varianza global de la desigualdad radica en la disputa distributiva entre la cúspide ($D_{10}$) y la base ($D_1-D_4$).

---

## 3. Registro de Transformaciones y Validaciones

| Paso de Transformación | Método Aplicado | Responsable | Validación |
| :--- | :--- | :--- | :--- |
| **Extracción DANE** | Consulta de microdatos y tablas de distribución decílica publicadas por el DANE. | Equipo Editorial | Cotejo contra Boletines Oficiales de Pobreza Monetaria. |
| **Cálculo de Palma** | División de participación porcentual de $D_{10}$ entre suma porcentual de $D_1$ a $D_4$. | Algoritmo determinístico | Verificado contra WDI y CEPALSTAT. |
| **Estandarización JSON/CSV** | Exportación a `data/palma_colombia_series.json` y `data/palma_colombia_series.csv`. | Agente de Gobernanza | Validación de esquema contra `palma_series.schema.json`. |
| **Redondeo Editorial** | Un decimal para el ratio ($3.7$), enteros para las galletas ($12, 43, 45$). | Protocolo Zero-Build | Cero *Lie Factor*, suma estricta a 100%. |

---

## 4. Limitaciones y Puntos Ciegos Declarados

1. **Flujo vs. Riqueza:** La GEIH mide flujos monetarios corrientes, no el stock acumulado de riqueza (bienes raíces, activos financieros, tenencia de tierras). El Gini de riqueza en Colombia supera el $0.85$.
2. **Subreporte en el Decil 10:** El percentil $99$ y $99.9$ no reporta ingresos de capital en encuestas de hogares presenciales, lo que subestima el Palma real en aproximadamente 1 a 1.5 puntos.
3. **Brechas Territoriales:** El indicador agregado nacional oculta disparidades departamentales extremas (ej. Chocó o La Guajira frente a Bogotá o Medellín).
