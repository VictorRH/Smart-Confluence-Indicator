# 📊 Chilaquil PRO Suite — V8.6

Suite de trading para TradingView (Pine Script v6) que combina **confluencia de indicadores**, **estructuras de precio** (patrones, Wyckoff, retrocesos, FVG), **mapas de liquidaciones** y **gestión de riesgo automática**.

Diseñado para traders nuevos y experimentados que buscan **menos falsas alarmas**, **múltiples fuentes de señal independientes** y **mejor control del riesgo**.

---

## ✨ ¿Qué hace?

La Suite integra 7 módulos que trabajan juntos:

| # | Módulo | Qué aporta |
|---|--------|-----------|
| 1 | **Núcleo de Señales** | Tendencia (EMAs auto por TF) + MACD + SQZMOM + RSI + filtros Breakout/Pivots + confirmación anti-repintado |
| 2 | **Heatmap de Liquidaciones** | Niveles estimados desde delta de Open Interest (estilo Coinglass), con auto-configuración por símbolo y temporalidad |
| 3 | **Liquidaciones Agregadas WW** | Histograma de liquidaciones REALES de 6 exchanges (Binance, Bybit, OKX, BitMEX, Deribit, HTX) |
| 4 | **Patrones de Chart** | HCH, Doble Techo, HCH Invertida y Doble Suelo: armado → proximidad a neckline → ruptura |
| 5 | **Wyckoff** | Spring, Upthrust, Test y Effort vs Result (eventos mecánicos, no subjetivos) |
| 6 | **Retrocesos** | Entrada anticipada en zona 0.50–0.65 de la pierna (Fibonacci) + vela de reacción |
| 7 | **FVG (Fair Value Gaps)** | Retorno a gaps de liquidez + reacción, con caducidad automática por temporalidad |

**Resultado:** cada módulo dispara sus propias señales, comparte la gestión de riesgo y reporta sus estadísticas por separado. 🎯

---

## 🚀 Características principales

### ✅ 2 Modos de operación (Señales)
- **Conservador**: RSI muy extremo (≤30 / ≥70) + tendencia simple — señales raras de alta convicción (triángulos 💠)
- **Equilibrado**: tendencia alineada + MACD + SQZMOM + RSI contextual (40–65 LONG / 35–60 SHORT) + Breakout — círculos

> Ambas familias de señales se dibujan SIEMPRE. El modo elegido define cuál maneja el estado de posición (SL/TP de la tabla) y las alertas principales.

### ✅ Gestión de riesgo integrada
- Stop Loss dinámico (ATR o %) — SL estructural **capado** por tu riesgo máximo
- Take Profit automático (basado en R/R)
- **Planes abiertos por módulo y lado**: un plan abierto por señal y lado (no doble conteo)
- **Supresión de entradas agotadas**: si el movimiento ya recorrió tu % objetivo (default 70% del camino al TP), no entran señales nuevas en ese lado (R/R invertido)
- **Caducidad de planes**: planes que no tocan SL/TP a tiempo se cierran a mercado (R parcial)
- Comisión por lado descontada del R neto (diagnóstico)

### ✅ Detección automática de temporalidad
- En Daily+ usa EMAs largas (100/200); en intraday EMAs cortas (7/15/25)
- Auto-ajuste de patrones, Wyckoff y retrocesos según TF
- Auto-configuración del heatmap: apalancamientos, resolución intrabar, escala y fecha de inicio

### ✅ Filtros anti-falsas-alarmas
1. **Breakout (L20)**: valida ruptura real
2. **Breakdown (L20)**: valida caída real
3. **Pivots**: evita entrar en resistencias/soportes
4. **RSI Contextual**: rango inteligente, no números fijos
5. **ADX** (opcional): evita rangos laterales
6. **Veto por liquidaciones**: bloquea entradas hacia clusters fuertes de liquidación cerca del stop
7. **Sesgo de TF superior (EMA200)** (opcional): alinea señales con la tendencia mayor

### ✅ Anti-repintado
- Señales confirmadas solo al **cierre de vela**
- Patrones/Wyckoff/FVG con pivotes confirmados + cierre
- Sesgo HTF con vela cerrada (sin lookahead)

---

## 📖 Guía para NOVATOS

### Instalación
1. Abre TradingView.com
2. Abre un gráfico (Bitcoin, acciones, forex, etc.)
3. Ve a "Indicadores" → "Pine Editor"
4. Copia TODO el código de `Chilaquil-Pro-Trading-System.pine`
5. Pega, guarda y añade al gráfico

### ¿Qué verás en el gráfico?
- **Letras de señales** sobre el gráfico: FR (Equilibrado), FV (Premium), FVG, UT, 2S, HCH, SP, T... (opcionalmente con figuras de colores si activas "Marcadores")
- **Heatmap de liquidaciones** en el precio: franjas amarillas = clusters con más liquidez
- **Panel inferior**: MACD + SQZMOM + Liquidaciones normalizados a la misma escala
- **Tablas de información**: estado del sistema + tabla de diagnóstico (planes, estadísticas por módulo)

### Tabla principal (resumen)

| Fila | Qué significa |
|------|---------------|
| Modo Señales | Conservador / Equilibrado (qué maneja estado y alertas) |
| EMAs Activas | Configuración usada (auto o manual) |
| RSI(14) | Valor actual |
| Tendencia / MACD / SQZMOM | Alcista / Bajista por indicador |
| Filtros | Breakout, Breakdown, Pivots, RSI contextual |
| Open Long/Short | Entrada del plan activo |
| SL / TP | Stop Loss y Take Profit |
| R/R | Relación Riesgo/Recompensa del plan |

### 📊 R/R (Reward/Risk)
- `1:2` = por cada $1 que arriesgas, ganas $2
- **Busca mínimo 1:1.5** ✅

### Flujo multi-TF recomendado (patrones)
1. **4H**: vigila las alertas de **ARMADO** (la formación se confirma ~5 velas después del hombro)
2. **1H**: espera la alerta de **ACERCÁNDOSE** a la neckline (armado → cercanía → ruptura)
3. **1H/15m**: usa **Retroceso o FVG** como gatillo fino cerca de la neckline
4. Opcional: activa "Sesgo de TF superior" (TF 240) para vetar señales de 1H contra la tendencia de 4H

> La TF mínima de patrones/Wyckoff/retrocesos/FVG es configurable (default **1H**). Las señales del núcleo están SIEMPRE activas en cualquier TF.

---

## ⚙️ Configuración recomendada para novatos

### Señales
- **Modo de Operación**: **Conservador** si empiezas (menos señales, mejor calidad); **Equilibrado** si ya tienes experiencia
- **Señales solo al cierre de vela**: ✅ Activado (anti-repintado)

### Gestión de Riesgo
- **Método**: Porcentaje
- **Stop Loss**: 3%
- **Multiplicador T/P (R/R)**: 2.0
- **Un plan abierto por módulo y lado**: ✅ Activado

### EMAs
- **Auto-Detectar Temporalidad**: ✅ Activado

### Mejoras (Filtros)
- **Filtro Breakout**: ✅ Activado
- **Filtro Pivots**: ✅ Activado

### Patrones / Wyckoff / Retrocesos / FVG
- Deja **🔧 Auto-ajuste por temporalidad** activado ✅
- **R/R objetivo**: 2.0

### Heatmap
- **🔧 Auto-Configurar**: ✅ Activado (ajusta símbolo + temporalidad automáticamente)

---

## 🎯 Cómo usar (Paso a paso)

### 1. Encuentra una señal
Cualquier módulo puede dispararla: núcleo (FR/FV), patrón (HCH, 2S...), Wyckoff (SP, T), retroceso o FVG.

### 2. Verifica el contexto
- ¿Tendencia, MACD y SQZMOM alineados?
- ¿Los filtros (Breakout, Pivots, RSI) están en 🟢?
- ¿Hay un cluster de liquidación justo delante? (si activaste el veto, el sistema ya lo bloquea)

### 3. Respeta la gestión de riesgo
- SL y TP quedan fijados al entrar: **no los muevas sin razón**
- El sistema suprime entradas tardías automáticamente (movimiento agotado)
- Espera TP, salida por cambio de tendencia, MACD contrario o RSI extremo (72/28)

---

## ⚠️ Disclaimer importante

**NO es garantía de ganancias:**
- Trading siempre tiene riesgo
- Los niveles del heatmap son **estimaciones** derivadas de OI, no datos de liquidaciones reales (esas están en el Módulo 3)
- Usa con DINERO DEMO primero
- Practica mínimo 2-4 semanas
- Nunca arriesgues dinero que no puedas perder

---

## 📊 Teoría detrás del sistema

### ¿Por qué confluencia?
Un indicador solo = ruido. Múltiples indicadores alineados = señal.

**El núcleo verifica:**
1. ¿La tendencia está clara? (EMAs)
2. ¿Hay momentum? (MACD)
3. ¿Hay presión real? (SQZMOM)
4. ¿El timing es bueno? (RSI)
5. ¿La ruptura es real? (Breakout/Breakdown)
6. ¿Es zona segura? (Pivots)

### ¿Por qué estructuras además de indicadores?
Patrones, Wyckoff, retrocesos y FVG son **fuentes de señal independientes**: si el núcleo falla, los demás módulos siguen generando oportunidades con su propia lógica y estadísticas.

### ¿Por qué el heatmap?
El precio suele ir a barrer la liquidez acumulada (stops y liquidaciones) antes de moverse de verdad. El sistema **veta entradas hacia clusters fuertes** cerca de tu stop: mejor no estar donde van a barrer.

---

## 🔧 Cómo optimizar

### Mercados rápidos (Forex, Crypto intradía)
- Usa **Conservador**
- Deja el auto-ajuste de patrones activado

### Mercados lentos (Acciones, Índices)
- Usa **Equilibrado**
- Activa **ADX** para filtrar laterales

### Intraday (1h–4h)
- EMAs automáticas ✅
- TF mínima de estructuras: 1H (default)

### Swing (Daily+)
- EMAs automáticas ✅
- Sube "Ancho de nivel" del heatmap a 0.15–0.30%

---

## 🤝 Contribuciones

¿Encontraste un bug? ¿Idea de mejora?

Abre un **Issue** o **Pull Request** en GitHub.

---

## 📞 Soporte

Este es un proyecto de código abierto. Lee el código, entiéndelo, úsalo con responsabilidad.

---

## 📝 Versión

- **V8.6** — Suite completa: ventana de dibujo solo reciente (FVG), alertas de proximidad a neckline, supresión de entradas agotadas, TF mínima 1H, fixes de heatmap y necklines
- **v4.2** — Fase 1: Breakout + RSI Contextual + Pivots (antiguo "Chilaquil PRO Trading System")

---

## ⭐ Si te fue útil

Dale una estrella en GitHub ⭐ para motivar desarrollo futuro.

---

**Creado con** ❤️ **para la comunidad de traders**

Happy Trading! 📈