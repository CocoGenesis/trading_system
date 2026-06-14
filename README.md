# 🦅 Trading System - Centro de Mando Hernani + VWAP/EMA9 Scanner

Sistema completo de trading paper (papel) con análisis técnico avanzado, alertas Telegram y dashboard terminal.

## 📦 Componentes

### 1. **Hernani - Centro de Mando V3.6**
- Análisis de correlación de mercado global
- Monitoreo de 28 pares (24 crypto + 9 acciones tokenizadas)
- Pulso de líderes (BTC, ETH, SOL)
- Alertas bidireccionales (LONG/SHORT)
- Patrón horario histórico (11 días de datos)

### 2. **VWAP + EMA9 Scanner**
- Detección de señales en 15m
- Cruces EMA9 + confirmación VWAP
- Paper trading engine
- Stop Loss inteligente con contexto Hernani
- Anti-duplicados con cooldown 120min

### 3. **Dashboard Terminal**
- Visualización en tiempo real (Rich library)
- Posiciones abiertas + historial
- Estadísticas PnL
- Integración Hernani
- Auto-refresh cada 10s

---

## 🚀 Instalación Rápida

### Paso 1: Clonar repositorio

```bash
git clone https://github.com/CocoGenesis/trading_system.git
cd trading_system
```

### Paso 2: Instalar dependencias

```bash
pip install -r requirements.txt
```

### Paso 3: Configurar credenciales

```bash
cp config.env.template config.env
nano config.env
```

Rellena con tus credenciales:
```env
# BITGET
API_KEY=tu_api_key
API_SECRET=tu_api_secret
API_PASSWORD=tu_password

# TELEGRAM (opcional pero recomendado)
TELEGRAM_TOKEN=tu_bot_token
TELEGRAM_CHAT_ID=tu_chat_id
```

### Paso 4: Crear carpeta de datos

```bash
mkdir -p data logs
```

---

## 🎯 Uso

### Ejecutar Centro de Mando Hernani

```bash
python3 hernani/centro_mando.py
```

Monitorea mercado global cada 60 segundos. Envía alertas Telegram cuando:
- Pulso LONG líderes cruza 55% (suave) → 2 snapshots (fuerte)
- Pulso SHORT líderes cruza 85% (suave) → 2 snapshots (fuerte)

### Ejecutar Scanner VWAP + EMA9

```bash
python3 scanner/vwap_ema9_scanner.py
```

Escanea 21 pares cada 2 minutos. Abre trades paper cuando:
- Precio cruza EMA9 hacia arriba + está sobre VWAP → **LONG**
- Precio cruza EMA9 hacia abajo + está bajo VWAP → **SHORT**

### Ver Dashboard

En otra terminal:
```bash
python3 dashboard/vwap_ema9_dashboard.py
```

Muestra en vivo:
- Posiciones abiertas (con PnL actual)
- Historial reciente
- Estadísticas (Win Rate, PnL total)
- Estado Hernani

---

## 📊 Archivos de Datos

```
data/
├── vwap_ema9_open.json          # Posiciones abiertas
├── vwap_ema9_trades.json        # Historial cerrados
├── vwap_ema9_status.json        # Último escaneo
├── estado_alertas.json          # Estado Hernani + contadores alertas
└── logs/
    ├── vwap_ema9.log            # Log general
    ├── scan_log_YYYY-MM-DD.csv  # Análisis diario
    └── hernani_historico_YYYYMMDD.csv  # Snapshots históricos
```

---

## ⚙️ Configuración Avanzada

### VWAP + EMA9 Scanner

```python
CAPITAL_TOTAL       = 200.0      # USDT simulados
MAX_POR_OPERACION   = 25.0       # USDT por trade
SL_PCT              = 1.5        # Stop Loss %
TP_PCT              = 3.0        # Take Profit %
MAX_OPEN_TRADES     = 8          # Posiciones simultáneas
CHECK_INTERVAL      = 120        # Segundos entre escaneos
TIMEFRAME           = "15m"      # Timeframe principal
```

### Hernani Centro de Mando

```python
ALERTA_SHORT_UMBRAL = 85.0       # % pulso SHORT para aviso
ALERTA_LONG_UMBRAL  = 55.0       # % pulso LONG para aviso
ALERTA_COOLDOWN_MIN = 30         # Minutos entre alertas
LOG_INTERVALO_MIN   = 30         # Guardar snapshot cada 30min
```

---

## 🔧 Troubleshooting

### Error: "No module named 'ccxt'"

```bash
pip install ccxt
```

### Error: "Telegram no configurado"

Las alertas Telegram son opcionales. Si no quieres usarlas:
- Deja `TELEGRAM_TOKEN` y `TELEGRAM_CHAT_ID` vacíos en `config.env`
- El sistema funcionará igual, solo sin alertas

### Error: "Rate limit exceeded"

Bitget tiene límites de API. Si ves este error:
- Aumenta `CHECK_INTERVAL` en scanner (ej: 180 segundos)
- Reduce cantidad de pares monitoreados
- Usa VPN si es necesario

---

## 📈 Filosofía de Operación

1. **Hernani** decide la dirección macro (LONG/SHORT/NEUTRO)
2. **Scanner** busca señales técnicas individuales
3. **Dashboard** muestra estado en vivo
4. **Paper Trading** simula ejecución sin riesgo real

El sistema NO ejecuta órdenes reales — solo simula en papel.

---

## 🤝 Autor

**CocoGenesis** — Sistema de trading paper para análisis técnico y educación.

---

## ⚠️ Disclaimer

Este es un sistema de **PAPER TRADING** (sin dinero real). Úsalo para:
- ✅ Aprender análisis técnico
- ✅ Backtestear estrategias
- ✅ Familiarizarte con el trading

**No uses dinero real sin entender completamente el sistema.**

---

## 📝 Changelog

### V3.6
- [NEW] Consolidación en estructura única
- [FIX] Eliminada duplicación de código
- [FIX] config.env centralizado
- [NEW] Módulos core reutilizables

### V3.5
- [NEW] Alertas Telegram bidireccionales
- [NEW] Persistencia de estado en disco

### V3.0+
- Centro de Mando Hernani
- VWAP + EMA9 Scanner
- Dashboard Terminal
