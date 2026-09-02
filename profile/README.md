# MERLIN

## HC2 · Panel ejecutivo de avance

> **MERLIN** desarrolla modelos energéticos georreferenciados para apoyar la planificación energética y la descarbonización territorial en Chile y Alemania.

**Corte:** 2 de septiembre de 2026  
**Fecha objetivo HC2:** 29 de octubre de 2026  
**Entrega del reporte técnico:** 29 de noviembre de 2026

## Estado general

**🛠️ N2/5 · HC2 en proceso: implementación y pilotos**

El avance se mide por madurez de evidencia, no por cantidad de código. Una celda país–sector alcanza el nivel HC2 únicamente cuando cuenta con modelo identificable, datos, ejecución reproducible, salida conservada y métrica de validación.

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

| Sector | Chile | Alemania | Próximo cierre |
|---|---|---|---|
| Residencial | **🛠️ N2** · Modelo térmico basado en Censo/SII y `tsib_fcr`; validación final pendiente | **📃 N1** · Datos LoD2/ALKIS y contrato de datos documentados; falta ejecutar el modelo | Caso reproducible con datos, clima, arquetipos y métricas |
| Comercial | **📃 N1** · Incluido en el modelo industrial-comercial; separación pendiente | **🛠️ N2** · Evidencia agregada en GHD; falta separar comercial y público | Definir frontera sectorial y fuente de validación |
| Público | **📃 N1** · Incluido dentro de servicios; separación pendiente | **⚠️ N0** · Aún no existe una celda público separada | Caso y fuente independiente o justificación metodológica |
| Industrial | **📊 N3** · Cadena RETC → energía → demanda térmica ejecutada y verificada | **✅ N4** · Piloto Baden-Württemberg: cobertura Industrie **1,03×** contra LAK×AGEB | Ampliar cobertura y cerrar métrica comparable HC2 |
| Transporte | **📊 N3** · Modelo LPV ejecutado y extendido a cuatro conurbaciones chilenas | **⚠️ N0** · Modelo alemán aún por adaptar | Caso alemán reproducible y validado |

> Los factores **1,03×** y **0,81×** son resultados de cobertura contra LAK×AGEB; no equivalen directamente a MAPE. La métrica exigida por HC2 debe consolidarse por país y sector.

## Avances recientes

- **Emisiones y demanda térmica:** `emission_model` publicó el motor core agnóstico de país y el adaptador de Baden-Württemberg.
- **Chile:** cadena RETC → energía → demanda térmica verificada con **8.893/8.893 filas idénticas** para 2024.
- **Baden-Württemberg:** cadena completa ejecutada con fuentes EU-ETS y LUBW; se excluye `Energiewirtschaft` de la demanda final.
- **Validación alemana:** cobertura de **1,03× en Industrie** y **0,81× en Haushalte + GHD** contra LAK ajustado por AGEB.
- **Transporte:** modelo de actividad vial LPV ampliado a Antofagasta, Concepción, La Serena–Coquimbo y Valparaíso.
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
| Demanda eléctrica | [`MERLIN_EDM`](https://github.com/FCR-CSET-Merlin/MERLIN_EDM) |
| Transporte | [`energy-road-transport-chile`](https://github.com/FCR-CSET-Merlin/energy-road-transport-chile) |
| H₂ y e-fuels | [`H2Integrate_CL`](https://github.com/FCR-CSET-Merlin/H2Integrate_CL) · [`h2v_tea`](https://github.com/FCR-CSET-Merlin/h2v_tea) |
| Datos y modelos alemanes | [`MERLIN_RCP_Alemania`](https://github.com/FCR-CSET-Merlin/MERLIN_RCP_Alemania) |

## Fuente de seguimiento

El detalle metodológico, la matriz de compromisos, la matriz de evidencia y la ruta de cierre se mantienen en [`merlin-index/08-reportaje-corfo`](https://github.com/FCR-CSET-Merlin/merlin-index/tree/main/08-reportaje-corfo).

**Regla de actualización:** cada cambio de estado debe enlazar a un repositorio, commit, caso reproducible, resultado o evidencia verificable. No se deben convertir avances de desarrollo en cumplimiento validado.
