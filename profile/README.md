# MERLIN

## HC2 · Panel ejecutivo de avance

> **MERLIN** desarrolla modelos energéticos georreferenciados para apoyar la planificación energética y la descarbonización territorial en Chile y Alemania.

**Corte:** 15 de septiembre de 2026<br>
**Fecha objetivo HC2:** 29 de octubre de 2026<br>
**Entrega del reporte técnico:** 29 de noviembre de 2026

## Estado general

**🛠️ N2/5 · HC2 en proceso: implementación y pilotos**

El avance se mide por madurez de evidencia, no por cantidad de código. Este corte incorpora los cambios fusionados hasta el 15 de septiembre de 2026; los PR abiertos se mantienen como trabajo pendiente. Una celda país–sector alcanza el nivel HC2 únicamente cuando cuenta con modelo identificable, datos, ejecución reproducible, salida conservada y métrica de validación.

### Escala de avance

| Indicador | Nivel | Interpretación ejecutiva |
|---|---:|---|
| ⚠️ | **N0 · No iniciado** | No existe todavía un caso o una adaptación verificable. |
| 📃 | **N1 · Base definida** | Existe plan, fuentes, arquitectura o documentación, pero no una ejecución reportable. |
| 🛠️ | **N2 · Implementado / piloto** | Hay código y un primer caso o integración, pero falta reproducibilidad completa o validación comparable. |
| 📊 | **N3 · Ejecutado** | El caso corre de forma reproducible y conserva una salida inspeccionable. |
| ✅ | **N4 · Validado** | Existe contraste cuantitativo con datos independientes y una métrica explícita. |
| 📒 | **N5 · Listo para HC2** | La celda país–sector cumple todos los requisitos de evidencia y puede reportarse. |
| ⛔ | **N6 · Bloqueado / problema a solucionar** | Existe un bloqueo o problema material que impide avanzar al siguiente nivel. |

| Dimensión | Nivel actual |
|---|---|
| Modelos chilenos prioritarios | **📊 N3** · Varios casos ejecutados; paquetes de evidencia y métricas en consolidación |
| Motor común Chile–Alemania | **🛠️ N2** · Publicado en `emission_model` |
| Piloto industrial alemán | **✅ N4** · Validado en Baden-Württemberg; 3/3 comparaciones de precisión con MAPE <35 % |
| Modelo residencial alemán | **📃 N1** · Datos y contrato en preparación |
| Modelo de transporte alemán | **✅ N4** · Piloto Múnich DE0–DE7b validado a nivel Kreis |
| Separación comercial / público | **📃 N1** · Brecha metodológica abierta |
| Métricas comparables por país–sector | **📊 N3** · Evidencia CORFO para emisiones y transporte; matriz completa pendiente |

## Matriz rápida de cobertura HC2

**Corte de la matriz:** 15 de septiembre de 2026. Los estados se asignan sólo a entregas versionadas en ramas principales o a paquetes de evidencia con resultados conservados; las ramas de reportabilidad pendientes de integración se identifican explícitamente.

| Sector | Chile | Alemania | Próximo cierre |
|---|---|---|---|
| Residencial | **🛠️ N2** · Modelo térmico basado en Censo/SII y `tsib_fcr`; la integración `MERLIN_RCP`–`tsib_fcr` sigue en el PR [#2](https://github.com/FCR-CSET-Merlin/MERLIN_RCP/pull/2) y la validación final está pendiente | **📃 N1** · Datos LoD2/ALKIS y contrato de datos documentados; falta ejecutar el modelo | Fusionar y validar el caso reproducible Chile; ejecutar el caso alemán con datos, clima, arquetipos y métricas |
| Comercial | **📃 N1** · Incluido en el modelo industrial-comercial; separación pendiente | **🛠️ N2** · Evidencia agregada en GHD; falta separar comercial y público | Definir frontera sectorial y fuente de validación |
| Público | **📃 N1** · Incluido dentro de servicios; separación pendiente | **⚠️ N0** · Aún no existe una celda público separada | Caso y fuente independiente o justificación metodológica |
| Industrial | **✅ N4** · `emission_model`: 8.893/8.893 filas verificadas y MAPE titular Chile 16,79–29,78 % | **✅ N4** · Piloto BW: 3/3 comparaciones de precisión con MAPE 10,90–13,88 %; cobertura Industrie **1,03×** | Ampliar cobertura y separar precisión, cobertura y representatividad |
| Transporte | **✅ N4** · Chile 2024: MAPE 25,1 %/26,8 % contra BNE, 10,3 %/12,9 % contra SEC y 18,0 % en dos conurbaciones | **✅ N4** · Múnich: MAPE 17,4 % a nivel de 13 Kreise; demanda no calibrada | Completar multi-año, diésel, EOD/STU y una referencia independiente de mayor resolución |

> Los factores **1,03×** y **0,81×** son resultados de cobertura contra LAK×AGEB; no equivalen directamente a MAPE. La métrica exigida por HC2 debe consolidarse por país y sector.

## Avances recientes

- **Emisiones y demanda térmica:** `emission_model` publicó el motor core agnóstico de país, los adaptadores Chile/Baden-Württemberg y una validación chilena cobertura-consciente en tres niveles frente a BNE e INGEI.
- **Chile:** cadena RETC → energía → demanda térmica verificada con **8.893/8.893 filas idénticas** para 2024; los KPI titulares del paquete CORFO reportan MAPE 29,64 %, 16,79 % y 29,78 %.
- **Baden-Württemberg:** cadena completa ejecutada con fuentes EU-ETS y LUBW; se excluye `Energiewirtschaft` de la demanda final. Las tres comparaciones de precisión del paquete CORFO cumplen MAPE <35 %.
- **Validación alemana:** cobertura de **1,03× en Industrie** y **0,81× en Haushalte + GHD** contra LAK ajustado por AGEB.
- **Transporte:** `main` integra el piloto alemán DE0–DE7b para Múnich; el paquete CORFO reporta MAPE 17,4 % a nivel Kreis contra FZJ y APE 0,6 %/7,6 % contra BAFA.
- **Paquetes CORFO:** `emission_model/corfo-report` está en `main`; `energy-road-transport-chile/corfo-report` está versionado en la rama `chore/corfo-report-structure` mientras se revisa su integración.
- **Bombas de calor:** `hp_residential_sim` incorporó optimización horaria industrial y residencial ACS, selección batch por edificio y exportación de manifiestos; el repositorio contiene pruebas automatizadas, pero su integración con el flujo residencial principal aún está pendiente.
- **H₂ y e-fuels:** `H2Integrate_CL` fusionó dos casos DOE Chile para Antofagasta y Magallanes con recursos meteorológicos públicos 2023, manifiesto de procedencia y verificación de integridad.
- **Datos alemanes:** adquisición reproducible de datos LoD2 y ALKIS documentada para Colonia/NRW.
- **Gobernanza:** `merlin-index` incorpora la matriz de evidencia y el flujo de cierre para el reporte CORFO.

## Brechas críticas para HC2

| Brecha | Resultado requerido | Responsable principal |
|---|---|---|
| Cobertura de modelos por país y sector | Completar las celdas aún N0/N1 con un caso reproducible | Responsables de cada modelo |
| Separación comercial / público | Definición sectorial, fuente y método de validación | Pablo + Raimundo / Cristóbal |
| Métricas comparables | MAPE u otra métrica justificada por celda país–sector | Cada responsable |
| Contratos de datos | Unidades, períodos, clima, escalas espaciales e identificadores comunes | Pablo + Cristóbal + Raimundo |
| Continuidad de conocimiento RETC y bombas de calor | Inventario, caso reproducible y sucesor técnico | Pablo + responsables por confirmar |

## Ruta de cierre

- [x] Identificar modelos chilenos y responsables.
- [x] Publicar motor común y primer adaptador alemán.
- [x] Ejecutar piloto industrial en Baden-Württemberg.
- [x] Documentar fuentes LoD2/ALKIS para Alemania.
- [x] Extender el modelo LPV a cinco conurbaciones.
- [x] Integrar y cerrar la validación 2024 del modelo de transporte.
- [x] Incorporar validación chilena cobertura-consciente BNE + INGEI.
- [x] Incorporar casos DOE Chile y recursos meteorológicos públicos en `H2Integrate_CL`.
- [x] Completar el piloto alemán de transporte DE0–DE7b; DE6 queda diferida y DE8 fuera de alcance.
- [x] Ejecutar validaciones y métricas comparables para los pilotos industrial BW y transporte Chile/Múnich.
- [ ] Definir matriz definitiva de cobertura país–sector.
- [ ] Completar modelo residencial alemán.
- [ ] Separar comercial y público.
- [ ] Congelar casos, datos, parámetros y contratos.
- [ ] Consolidar paquete de evidencia para el informe técnico.

## Repositorios clave

| Área | Repositorio |
|---|---|
| Índice, evidencia y seguimiento | [`merlin-index`](https://github.com/FCR-CSET-Merlin/merlin-index) |
| Emisiones y demanda térmica | [`emission_model`](https://github.com/FCR-CSET-Merlin/emission_model) · [`corfo-report`](https://github.com/FCR-CSET-Merlin/emission_model/tree/main/corfo-report) |
| Demanda residencial | [`MERLIN_RCP`](https://github.com/FCR-CSET-Merlin/MERLIN_RCP) · [`tsib_fcr`](https://github.com/FCR-CSET-Merlin/tsib_fcr) |
| Bombas de calor | [`hp_residential_sim`](https://github.com/FCR-CSET-Merlin/hp_residential_sim) · [`tea_heat_pumps`](https://github.com/FCR-CSET-Merlin/tea_heat_pumps) |
| Demanda eléctrica | [`MERLIN_EDM`](https://github.com/FCR-CSET-Merlin/MERLIN_EDM) |
| Transporte | [`energy-road-transport-chile`](https://github.com/FCR-CSET-Merlin/energy-road-transport-chile) · [`corfo-report`](https://github.com/FCR-CSET-Merlin/energy-road-transport-chile/tree/chore/corfo-report-structure/corfo-report) |
| H₂ y e-fuels | [`H2Integrate_CL`](https://github.com/FCR-CSET-Merlin/H2Integrate_CL) · [`h2v_tea`](https://github.com/FCR-CSET-Merlin/h2v_tea) |
| Datos y modelos alemanes | [`MERLIN_RCP_Alemania`](https://github.com/FCR-CSET-Merlin/MERLIN_RCP_Alemania) |

## Fuente de seguimiento

El detalle metodológico, la matriz de compromisos, la matriz de evidencia y la ruta de cierre se mantienen en [`merlin-index/08-reportaje-corfo`](https://github.com/FCR-CSET-Merlin/merlin-index/tree/main/08-reportaje-corfo).

**Regla de actualización:** cada cambio de estado debe enlazar a un repositorio, commit, caso reproducible, resultado o evidencia verificable. No se deben convertir avances de desarrollo en cumplimiento validado.
