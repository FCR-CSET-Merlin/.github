# MERLIN

## HC2 · Panel ejecutivo de avance

> **MERLIN** desarrolla modelos energéticos georreferenciados para apoyar la planificación energética y la descarbonización territorial en Chile y Alemania.

**Corte:** 3 de septiembre de 2026  
**Fecha objetivo HC2:** 29 de octubre de 2026  
**Entrega del reporte técnico:** 29 de noviembre de 2026

## Estado general

**🛠️ N2/5 · HC2 en proceso: implementación y pilotos**

El avance se mide por madurez de evidencia, no por cantidad de código. Este corte incorpora los cambios fusionados hasta el 3 de septiembre de 2026; los PR abiertos se mantienen como trabajo pendiente. Una celda país–sector alcanza el nivel HC2 únicamente cuando cuenta con modelo identificable, datos, ejecución reproducible, salida conservada y métrica de validación.

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
| Modelos chilenos principales identificados | **📃 N1** · Base disponible |
| Motor común Chile–Alemania | **🛠️ N2** · Publicado en `emission_model` |
| Piloto industrial alemán | **✅ N4** · Validado en Baden-Württemberg |
| Modelo residencial alemán | **📃 N1** · Datos y contrato en preparación |
| Modelo de transporte alemán | **⚠️ N0** · Adaptación pendiente |
| Separación comercial / público | **📃 N1** · Brecha metodológica abierta |
| Métricas comparables por país–sector | **📃 N1** · En consolidación |

## Matriz rápida de cobertura HC2

**Corte de la matriz:** 3 de septiembre de 2026. Los estados se asignan sólo a
entregas versionadas en la rama principal; los resultados que viven en PR abiertos
se muestran como pendientes de integración.

| Sector | Chile | Alemania | Próximo cierre |
|---|---|---|---|
| Residencial | **🛠️ N2** · Modelo térmico basado en Censo/SII y `tsib_fcr`; la integración `MERLIN_RCP`–`tsib_fcr` sigue en el PR [#2](https://github.com/FCR-CSET-Merlin/MERLIN_RCP/pull/2) y la validación final está pendiente | **📃 N1** · Datos LoD2/ALKIS y contrato de datos documentados; falta ejecutar el modelo | Fusionar y validar el caso reproducible Chile; ejecutar el caso alemán con datos, clima, arquetipos y métricas |
| Comercial | **📃 N1** · Incluido en el modelo industrial-comercial; separación pendiente | **🛠️ N2** · Evidencia agregada en GHD; falta separar comercial y público | Definir frontera sectorial y fuente de validación |
| Público | **📃 N1** · Incluido dentro de servicios; separación pendiente | **⚠️ N0** · Aún no existe una celda público separada | Caso y fuente independiente o justificación metodológica |
| Industrial | **📊 N3** · Cadena RETC → energía → demanda térmica ejecutada y verificada; `emission_model` añadió validación cobertura-consciente BNE + INGEI, sin convertir la cobertura parcial en validación plena | **✅ N4** · Piloto Baden-Württemberg: cobertura Industrie **1,03×** contra LAK×AGEB | Ampliar cobertura y cerrar métrica comparable HC2 |
| Transporte | **📊 N3** · Modelo LPV ejecutado para **cinco conurbaciones**; la validación 2024 está documentada en el PR [#4](https://github.com/FCR-CSET-Merlin/energy-road-transport-chile/pull/4), todavía abierto | **⚠️ N0** · Modelo alemán aún por adaptar | Integrar/revisar el PR de validación Chile y ejecutar un caso alemán reproducible y validado |

> Los factores **1,03×** y **0,81×** son resultados de cobertura contra LAK×AGEB; no equivalen directamente a MAPE. La métrica exigida por HC2 debe consolidarse por país y sector.

## Avances recientes

- **Emisiones y demanda térmica:** `emission_model` publicó el motor core agnóstico de país, los adaptadores Chile/Baden-Württemberg y una validación chilena cobertura-consciente en tres niveles frente a BNE e INGEI.
- **Chile:** cadena RETC → energía → demanda térmica verificada con **8.893/8.893 filas idénticas** para 2024; la nueva validación reporta una cobertura `structural_core` de **16,8 %** en el ámbito industrial y **29,8 %** en el total nacional, por debajo del umbral de 35 % definido para ese KPI.
- **Baden-Württemberg:** cadena completa ejecutada con fuentes EU-ETS y LUBW; se excluye `Energiewirtschaft` de la demanda final.
- **Validación alemana:** cobertura de **1,03× en Industrie** y **0,81× en Haushalte + GHD** contra LAK ajustado por AGEB.
- **Transporte:** el modelo LPV fue extendido a **cinco conurbaciones** y cuenta con validación 2024: MAPE **25,1 %** del modelo comunal calibrado contra BNE regional, **10,3 %** contra ventas SEC totales por conurbación y **18,0 %** en el cruce con BNE regional. El PR [#4](https://github.com/FCR-CSET-Merlin/energy-road-transport-chile/pull/4) sigue abierto y no se considera integrado hasta su revisión.
- **Bombas de calor:** `hp_residential_sim` incorporó optimización horaria industrial y residencial ACS, selección batch por edificio y exportación de manifiestos; el repositorio contiene pruebas automatizadas, pero su integración con el flujo residencial principal aún está pendiente.
- **H₂ y e-fuels:** `H2Integrate_CL` fusionó dos casos DOE Chile para Antofagasta y Magallanes con recursos meteorológicos públicos 2023, manifiesto de procedencia y verificación de integridad.
- **Datos alemanes:** adquisición reproducible de datos LoD2 y ALKIS documentada para Colonia/NRW.
- **Gobernanza:** `merlin-index` incorpora la matriz de evidencia y el flujo de cierre para el reporte CORFO.

## Brechas críticas para HC2

| Brecha | Resultado requerido | Responsable principal |
|---|---|---|
| Adaptación de modelos a Alemania | Al menos un caso ejecutado y reproducible por sector | Responsables de cada modelo |
| Separación comercial / público | Definición sectorial, fuente y método de validación | Pablo + Raimundo / Cristóbal |
| Métricas comparables | MAPE u otra métrica justificada por celda país–sector | Cada responsable |
| Contratos de datos | Unidades, períodos, clima, escalas espaciales e identificadores comunes | Pablo + Cristóbal + Raimundo |
| Continuidad de conocimiento RETC y bombas de calor | Inventario, caso reproducible y sucesor técnico | Pablo + responsables por confirmar |

## Ruta de cierre

- [x] Identificar modelos chilenos y responsables.
- [x] Publicar motor común y primer adaptador alemán.
- [x] Ejecutar piloto industrial en Baden-Württemberg.
- [x] Documentar fuentes LoD2/ALKIS para Alemania.
- [x] Extender el modelo LPV a cinco conurbaciones y documentar su validación 2024.
- [x] Incorporar validación chilena cobertura-consciente BNE + INGEI.
- [x] Incorporar casos DOE Chile y recursos meteorológicos públicos en `H2Integrate_CL`.
- [ ] Revisar y cerrar el PR [#4 de transporte](https://github.com/FCR-CSET-Merlin/energy-road-transport-chile/pull/4).
- [ ] Definir matriz definitiva de cobertura país–sector.
- [ ] Completar modelo residencial alemán.
- [ ] Completar adaptación alemana de transporte.
- [ ] Separar comercial y público.
- [ ] Ejecutar validaciones y métricas comparables.
- [ ] Congelar casos, datos, parámetros y contratos.
- [ ] Consolidar paquete de evidencia para el informe técnico.

## Repositorios clave

| Área | Repositorio |
|---|---|
| Índice, evidencia y seguimiento | [`merlin-index`](https://github.com/FCR-CSET-Merlin/merlin-index) |
| Emisiones y demanda térmica | [`emission_model`](https://github.com/FCR-CSET-Merlin/emission_model) |
| Demanda residencial | [`MERLIN_RCP`](https://github.com/FCR-CSET-Merlin/MERLIN_RCP) · [`tsib_fcr`](https://github.com/FCR-CSET-Merlin/tsib_fcr) |
| Bombas de calor | [`hp_residential_sim`](https://github.com/FCR-CSET-Merlin/hp_residential_sim) · [`tea_heat_pumps`](https://github.com/FCR-CSET-Merlin/tea_heat_pumps) |
| Demanda eléctrica | [`MERLIN_EDM`](https://github.com/FCR-CSET-Merlin/MERLIN_EDM) |
| Transporte | [`energy-road-transport-chile`](https://github.com/FCR-CSET-Merlin/energy-road-transport-chile) |
| H₂ y e-fuels | [`H2Integrate_CL`](https://github.com/FCR-CSET-Merlin/H2Integrate_CL) · [`h2v_tea`](https://github.com/FCR-CSET-Merlin/h2v_tea) |
| Datos y modelos alemanes | [`MERLIN_RCP_Alemania`](https://github.com/FCR-CSET-Merlin/MERLIN_RCP_Alemania) |

## Fuente de seguimiento

El detalle metodológico, la matriz de compromisos, la matriz de evidencia y la ruta de cierre se mantienen en [`merlin-index/08-reportaje-corfo`](https://github.com/FCR-CSET-Merlin/merlin-index/tree/main/08-reportaje-corfo).

**Regla de actualización:** cada cambio de estado debe enlazar a un repositorio, commit, caso reproducible, resultado o evidencia verificable. No se deben convertir avances de desarrollo en cumplimiento validado.
