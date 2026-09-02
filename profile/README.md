# MERLIN

## HC2 · Panel ejecutivo de avance

> **MERLIN** desarrolla modelos energéticos georreferenciados para apoyar la planificación energética y la descarbonización territorial en Chile y Alemania.

**Corte:** 2 de septiembre de 2026  
**Fecha objetivo HC2:** 29 de octubre de 2026  
**Entrega del reporte técnico:** 29 de noviembre de 2026

## Estado general

🟡 **HC2 en proceso: adaptación y validación de modelos para Alemania**

El criterio de avance no es la existencia de código por sí sola. Una celda país–sector se considera cubierta cuando cuenta con un modelo identificable, datos, ejecución reproducible, salida conservada y una métrica de validación.

| Dimensión | Estado |
|---|---|
| Modelos chilenos principales identificados | ✅ Base disponible |
| Motor común Chile–Alemania | ✅ Publicado en `emission_model` |
| Piloto industrial alemán | ✅ Ejecutado y contrastado en Baden-Württemberg |
| Modelo residencial alemán | 🟡 Datos y contrato en preparación |
| Modelo de transporte alemán | 🔴 Adaptación pendiente |
| Separación comercial / público | 🔴 Brecha metodológica abierta |
| Métricas comparables por país–sector | 🟡 En consolidación |

## Matriz rápida de cobertura HC2

| Sector | Chile | Alemania | Próximo cierre |
|---|---|---|---|
| Residencial | 🟡 Modelo térmico basado en Censo/SII y `tsib_fcr`; validación final pendiente | 🟡 Datos LoD2/ALKIS y contrato de datos documentados; falta ejecutar el modelo | Caso reproducible con datos, clima, arquetipos y métricas |
| Comercial | 🟡 Incluido en el modelo industrial-comercial; separación pendiente | 🟡 Evidencia agregada en GHD; falta separar comercial y público | Definir frontera sectorial y fuente de validación |
| Público | 🟡 Incluido dentro de servicios; separación pendiente | 🔴 Aún no separado de GHD | Caso y fuente independiente o justificación metodológica |
| Industrial | 🟡 Cadena RETC → energía → demanda térmica verificada | 🟡 Piloto Baden-Württemberg: cobertura Industrie **1,03×** contra LAK×AGEB | Ampliar cobertura y cerrar métrica comparable HC2 |
| Transporte | 🟡 Modelo LPV extendido a cuatro conurbaciones chilenas | 🔴 Modelo alemán aún por adaptar | Caso alemán reproducible y validado |

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
