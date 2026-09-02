# Centro Quant C v1.0 · Humano + Máquina — 2026-08-31

Base congelada: `Centro_Quant_B_v1_2_QRA09_Lab_2026-08-30.zip`.

## Objetivo del experimento
Comparar una ejecución automática (Quant B) contra una candidata semiautomática (Quant C) manteniendo las mismas reglas operativas de la base. La única variable nueva de C es la intervención humana de salida.

## Qué cambia en C
- Namespace independiente `quantc_`: no comparte ledger ni configuración con Quant B.
- Panel **Mesa Humano + Máquina** para ver entrada, precio, R actual, MFE, MAE y duración.
- Botón **Cerrar ahora**. Al pulsarlo intenta capturar el ticker actual de Binance y registra el cierre como `manual`.
- Cada cierre manual crea automáticamente una **sombra contrafactual** que continúa con las reglas automáticas originales hasta stop/objetivo.
- El panel calcula el delta entre el cierre humano y el resultado automático contrafactual cuando éste termina.

## Qué NO cambia
- Señales y score de la base.
- Lógica causal de entrada.
- Stops/objetivos automáticos de la base.
- QRA-05, QRA-06 y QRA-09 heredados de B.
- Seguimiento automático de posiciones.

## Regla de evidencia
Los cierres humanos quedan identificados por `status: "manual"` y `manualIntervention.version: "C-HUMAN-INTERVENTION-V1"`. Sus contrafactuales viven en el ledger de sombras con `cHumanCounterfactual: true`, por lo que no deben mezclarse con el ledger operativo principal.

Para una comparación limpia B vs C, ejecutar ambos prospectivamente y no modificar reglas adicionales durante la muestra.


## v6.11.7-C1.1-HUMAN
- Panel de intervención humana: añade columnas Stop y Objetivo usando los niveles originales guardados en cada operación.
- No cambia reglas de entrada, salida, R, MFE/MAE ni el namespace de datos; es un cambio visual de auditoría.
