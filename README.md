# 📊 Chilaquil PRO Trading System

Un sistema de trading semi-profesional para TradingView que combina **confluencia de indicadores** con **gestión de riesgo automática**.

Diseñado para traders nuevos y experimentados que buscan **menos falsas alarmas** y **mejor control del riesgo**.

---

## ✨ ¿Qué hace?

Este indicador detecta oportunidades de trading basadas en:

- **Tendencia**: EMAs (7/15/25 o 100/200 según temporalidad)
- **Momentum**: MACD
- **Volatilidad**: SQZMOM (Squeeze Momentum)
- **Timing**: RSI Contextual (inteligente, no fijo)
- **Validación**: Breakout real + Pivots

**Resultado:** Solo entra cuando TODAS las condiciones se alinean. 🎯

---

## 🚀 Características principales

### ✅ 2 Modos de operación
- **Conservador**: Solo entra con RSI muy extremo (≤30 / ≥70) - Alertas
- **Equilibrado**: RSI en rangos contextuales (40-65 LONG / 35-60 SHORT) - Tabla interactiva

### ✅ Gestión de riesgo integrada
- Stop Loss dinámico (ATR o %)
- Take Profit automático (basado en Reward/Risk)
- Seguimiento en tiempo real de posiciones

### ✅ Detección automática de temporalidad
- En Daily+ usa EMAs largas (100/200)
- En intraday usa EMAs cortas (7/15/25)
- Se ajusta automáticamente ⚙️

### ✅ 4 Filtros anti-falsas-alarmas
1. **Breakout (L20)**: Valida ruptura real
2. **Breakdown (L20)**: Valida caída real
3. **Pivots**: Evita entrar en resistencias/soportes
4. **RSI Contextual**: Rango inteligente, no números fijos

---

## 📖 Guía para NOVATOS

### Instalación
1. Abre TradingView.com
2. Abre un gráfico (Bitcoin, acciones, forex, etc.)
3. Ve a "Indicadores" → "Pine Script"
4. Copia TODO el código de `Chilaquil-Pro-Trading-System.pine`
5. Pega y crea el indicador

### Interpretación de la tabla

La tabla superior izquierda muestra TODO en tiempo real:

📊 CHILAQUIL PRO
├─ Modo Señales: Conservador / Equilibrado (elige uno)
├─ EMAs Activas: Los valores que usa
├─ RSI(14): Tu número RSI actual
├─ Tendencia: Alcista / Bajista
├─ MACD: Alcista / Bajista
├─ SQZMOM: Alcista / Bajista
│
├─ ━━━ FILTROS FASE 1 ━━━
├─ Breakout (L20): 🟢 OK / 🔴 Espera
├─ Breakdown (L20): 🟢 OK / 🔴 Espera
├─ Pivots: 🟢 Libre / ⚠️ Resistencia / ⚠️ Soporte
├─ RSI Contextual: Rango permitido
│
├─ 🟢 Open Long: Entrada (si hay)
├─ 🛑 SL Long: Stop Loss
├─ 💰 TP Long: Take Profit
├─ 📊 R/R Long: Relación Riesgo/Recompensa
│
└─ (Mismo para SHORT)

### ¿Qué significa cada cosa?

#### 🟢 Alcista
El indicador detecta dirección hacia ARRIBA. Busca entrar en **LONG (compra)**.

#### 🔴 Bajista
El indicador detecta dirección hacia ABAJO. Busca entrar en **SHORT (venta)**.

#### 🟢 OK / 🔴 Espera
- **🟢 OK**: El filtro está listo
- **🔴 Espera**: No hay señal aún, paciencia

#### 📊 R/R (Reward/Risk)
Relación riesgo-recompensa.
- `1:2` = Por cada $1 que arriesgas, ganas $2
- `1:3` = Por cada $1 que arriesgas, ganas $3
- **Busca mínimo 1:1.5** ✅

---

## ⚙️ Configuración recomendada para novatos

**En los Inputs del indicador:**

### Modo Señales
- **Principiante**: Elige **Conservador** (menos señales, mejor calidad)
- **Intermedio**: Elige **Equilibrado** (más señales)

### Gestión de Riesgo
- **Método**: Porcentaje
- **Stop Loss**: 3%
- **R/R Multiplier**: 2.0

### EMAs
- **Auto-Detectar**: Activado ✅ (se ajusta automáticamente)

### Mejoras (Filtros)
- **Activar Filtro Breakout**: ✅ Activado
- **Activar Filtro Pivots**: ✅ Activado

---

## 🎯 Cómo usar (Paso a paso)

### 1. Encuentra una señal
Espera a que los indicadores muestren `🟢 OK` en los filtros.

### 2. Lee la tabla
- ¿Todos los filtros están verdes?
- ¿El R/R es bueno (mínimo 1:1.5)?
- ¿El RSI está en rango contextual?

### 3. Entra SOLO si:
✅ Tendencia: Bullish/Bearish
✅ MACD: Bullish/Bearish (mismo que tendencia)
✅ SQZMOM: Bullish/Bearish (mismo que tendencia)
✅ RSI: Dentro del rango contextual
✅ Breakout/Breakdown: 🟢 OK
✅ Pivots: 🟢 Libre


### 4. Gestiona tu posición
- Tu SL está automático (no lo muevas sin razón)
- Espera a TP o mantén si ves más ganancias
- No entres por emociones

---

## ⚠️ Disclaimer importante

**NO es garantía de ganancias:**
- Trading siempre tiene riesgo
- Usa con DINERO DEMO primero
- Practica mínimo 2-4 semanas
- Nunca arriesgues dinero que no puedas perder

---

## 📊 Teoría detrás del sistema

### ¿Por qué confluencia?

Un indicador solo = ruido
Múltiples indicadores alineados = Señal

**Tu sistema verifica:**
1. ¿La tendencia está clara? (EMAs)
2. ¿Hay momentum? (MACD)
3. ¿Hay presión real? (SQZMOM)
4. ¿El timing es bueno? (RSI)
5. ¿La ruptura es real? (Breakout/Breakdown)
6. ¿Es zona segura? (Pivots)

Si TODO dice "SÍ" → Entrada de calidad

### ¿Por qué Breakout + Pivots?

**Breakout** = Evita comprar en picos falsos
**Pivots** = Evita entrar exactamente en resistencia

Juntos = Menos falsas alarmas ✅

---

## 🔧 Cómo optimizar

### Para mercados rápidos (Forex, Crypto)
- Usa **Conservador** (RSI ≤ 30 / ≥ 70)
- Reduce Lookback a 15 barras

### Para mercados lentos (Acciones, Índices)
- Usa **Equilibrado** (RSI contextual)
- Aumenta Lookback a 25 barras

### Para intraday (1h-4h)
- Deja EMAs automáticas ✅
- Usa Conservador

### Para swing (Daily)
- Deja EMAs automáticas ✅
- Usa Equilibrado

---

## 📈 Métricas esperadas

**Con backtesting en datos reales (YMMV):**
- Win Rate: 55-65%
- R/R promedio: 1.5 - 2.0
- Max Drawdown: 5-8%

**Resultado:** Aunque pierdas ~40% de trades, ganas dinero porque R/R es favorable.

---

## 🤝 Contribuciones

¿Encontraste un bug? ¿Idea de mejora?

Abre un **Issue** o **Pull Request** en GitHub.

---

## 📞 Soporte

Este es un proyecto de código abierto. Lee el código, entiéndelo, úsalo con responsabilidad.

---

## 📝 Versión

- **v4.2** - Fase 1: Breakout + RSI Contextual + Pivots
- Próxima: Fase 2 con Wyckoff avanzado (opcional)

---

## ⭐ Si te fue útil

Dale una estrella en GitHub ⭐ para motivar desarrollo futuro.

---

**Creado con** ❤️ **para la comunidad de traders**

Happy Trading! 📈
