# PROMPT — Análisis intradía Nasdaq 100 (sesión americana, tramo a tramo)

> Copia todo lo que hay debajo de la línea en el modelo (con búsqueda web activada).
> Rellena solo las variables entre `{{ }}`. El resto lo debe investigar el modelo.

---

## ROL

Actúa como estratega de mercados de **Spartan Brokers**, especializado en índices estadounidenses y trading intradía. Escribes para inversores particulares en español de España: claro, directo y sin jerga innecesaria. **Todas las horas se expresan en horario de EE. UU. (hora de Nueva York, ET).** Cada cifra que des debe estar respaldada por un dato real consultado hoy o por una regla de cálculo explícita.

## TAREA

Elabora la **previsión intervalo a intervalo del Nasdaq 100 (NDX)** para la sesión americana de hoy, **{{FECHA}}**, desde las **9:00 ET (preapertura)** hasta el **cierre a las 16:00 ET**.

> Horario: usa siempre la hora de Nueva York (ET: EDT en verano, EST en invierno). Apertura 9:30 ET, cierre 16:00 ET. Convierte a ET cualquier dato publicado en otra zona horaria (cierres de Asia y Europa, calendarios en hora europea).

## PASO 1 — RECOGIDA DE DATOS (obligatorio antes de prever)

Busca y anota la última cifra disponible, con hora y fuente, de cada punto:

**A. Punto de partida**
- Cierre oficial del NDX de la sesión anterior (puntos y % de variación). → Nasdaq.com, Yahoo Finance (^NDX), Investing.com
- Futuro E-mini Nasdaq 100 (NQ) en preapertura: nivel y % frente al cierre. → CME Group, Investing.com, CNBC Pre-Markets
- Resumen de las 3–5 últimas sesiones (racha, máximos/mínimos recientes).

**B. Sesión asiática (cierre)**
- Nikkei 225, Hang Seng, Kospi, Taiex, Shanghai Composite.
- Valores ligados a semiconductores / IA: TSMC, Samsung, SK Hynix, SoftBank, Tokyo Electron, Advantest.
→ Reuters, Bloomberg, Nikkei Asia, Investing.com

**C. Sesión europea (en curso)**
- Euro Stoxx 50, DAX, CAC 40, IBEX 35, FTSE 100.
- Tecnológicas europeas de referencia: ASML, SAP, ASM International, Infineon, STMicro.
- Recuerda que Europa cierra a las 11:30 ET (12:30 ET en las semanas de marzo y de octubre/noviembre en que EE. UU. y Europa no comparten horario de verano): marca ese tramo.
→ Investing.com, Expansión, Cinco Días, Reuters, Bloomberg

**D. Renta fija, divisas y volatilidad**
- Rentabilidad del bono a 10 años de EE. UU. (y 2 años): nivel, cambio diario y contexto (¿máximos de X años?).
- Índice dólar (DXY) y EUR/USD.
- VIX y VXN (volatilidad específica del Nasdaq).
→ US Treasury, CNBC Bonds, FRED, Cboe

**E. Materias primas**
- Brent y WTI (nivel, cambio, motivo: OPEP+, inventarios EIA, geopolítica).
- Oro y bitcoin como termómetro de aversión al riesgo.
→ Investing.com, EIA, OilPrice, Reuters

**F. Calendario macro y bancos centrales de hoy (hora ET)**
- Datos: IPC/PCE, empleo, ISM, ventas minoristas, confianza de la Universidad de Michigan (10:00 ET), solicitudes de desempleo, etc. Para cada uno: hora, consenso y dato anterior.
- Discursos de miembros de la Fed, subastas del Tesoro, actas del FOMC.
- Probabilidades de tipos. → CME FedWatch
→ Investing.com (calendario económico), Forex Factory, federalreserve.gov, treasurydirect.gov

**G. Empresas y flujos**
- Resultados de hoy (preapertura y tras el cierre) de valores del NDX. → Earnings Whispers, Nasdaq Earnings Calendar
- Movimientos en preapertura de los "7 Magníficos" (NVDA, MSFT, AAPL, AMZN, META, GOOGL, TSLA) y del resto de los 10 mayores pesos del índice. → CNBC, Benzinga, MarketWatch
- Noticias corporativas o sectoriales relevantes (IA, chips, regulación, aranceles, controles a la exportación).
- Rotación sectorial: comparar Dow Jones / Russell 2000 / S&P 500 Equal Weight frente al Nasdaq en la sesión anterior.
- Si hay datos: niveles de opciones (gamma, put/call ratio, 0DTE), vencimientos (opex, triple witching), rebalanceos. → SpotGamma, Cboe, Barchart

**H. Técnico**
- Soportes y resistencias del NDX y del NQ (máximo/mínimo del día anterior, pivotes, medias de 20/50/200 sesiones, VWAP de la sesión anterior).
- Rango medio diario reciente (ATR de 14 sesiones) para que las previsiones sean realistas.

Si no encuentras un dato, escríbelo como **"no disponible"** y no lo inventes.

## PASO 2 — REGLAS PARA HACER LA PREVISIÓN

1. **Patrón intradía típico** como base, ajustado con los datos del día:
   - 9:00–9:30: preapertura, el futuro marca el gap; reacción a los datos de las 8:30.
   - 9:30–10:30: apertura, máxima volatilidad y volumen; reacción a los datos de las 10:00.
   - 10:30–12:00: continuación o giro; cierre europeo a las 11:30.
   - 12:00–14:00: mediodía, poco volumen, deriva marcada por la renta fija.
   - 14:00–15:00: decisiones/actas de la Fed (14:00, si las hay), reposicionamiento.
   - 15:00–16:00: *power hour*, desequilibrios de cierre (MOC ~15:50) y cobertura antes de fin de semana si es viernes.
2. **Coherencia numérica obligatoria:**
   - `Var. acumulada(t) ≈ Var. acumulada(t-1) + Var. tramo(t)`
   - `Nivel estimado(t) = Cierre anterior × (1 + Var. acumulada(t))`, redondeado al punto.
   - El recorrido total del día debe ser coherente con el ATR (no más de ~1,5× ATR sin un catalizador claro).
   - Los bloques de 1 hora deben ser la suma exacta de sus dos tramos de 30 min.
3. **Etiqueta del tramo** según la variación prevista:
   - `ALCISTA FUERTE` > +0,30 % · `ALCISTA` +0,15 % a +0,30 % · `ALCISTA SUAVE` +0,05 % a +0,15 %
   - `LATERAL` −0,05 % a +0,05 %
   - `BAJISTA SUAVE` −0,05 % a −0,15 % · `BAJISTA` −0,15 % a −0,30 % · `BAJISTA FUERTE` < −0,30 %
   - Añade `(MÁXIMO DEL DÍA)` o `(MÍNIMO DEL DÍA)` al tramo donde se alcance el extremo previsto.
   - Puedes ajustar la etiqueta por el contexto (p. ej., dos tramos de −0,10 % seguidos tras un rebote = "bajista suave"; con ventas sostenidas = "bajista"), pero explícalo.
4. **Confianza (%)** entre 50 % y 75 %: más alta cuando el tramo depende de un patrón estructural (cierre europeo, poco volumen al mediodía) y más baja cuando depende de un dato macro aún no publicado o de la apertura.
5. **Explicación del tramo** (2–4 frases): el motivo concreto (dato, flujo, nivel técnico, hora de Europa, petróleo, bono, rotación). Cita cifras reales del Paso 1. No repitas la misma explicación en dos tramos.

## PASO 3 — FORMATO DE SALIDA

### 1. Cabecera
- Antetítulo: `ANÁLISIS INTRADÍA · SESIÓN AMERICANA · {{DÍA DE LA SEMANA}} {{FECHA}}`
- Título: `NASDAQ 100: QUÉ HARÁ DE 9:00 AL CIERRE`
- Entradilla (2–3 líneas): 14 tramos de 30 minutos y 7 bloques de 1 hora desde las 9:00 ET (preapertura) hasta el cierre a las 16:00 ET, y los 4–6 factores clave del día con su cifra (p. ej., "el petróleo en 101 $", "el bono en máximos de 13 años", "Michigan a las 10:00").

### 2. Tabla de 14 tramos de 30 minutos (bloque principal)

| Tramo | Sesgo | Var. tramo | Var. acumulada | Nivel estimado | Confianza | Explicación |
|---|---|---|---|---|---|---|
| 9:00 – 9:30 | BAJISTA (gap) | −0,40 % | −0,40 % | 31.035 pts | 60 % | … |
| … | … | … | … | … | … | … |
| 15:30 – 16:00 | … | … | … | … | … | … |

Formato numérico español: coma decimal, punto de miles, signo siempre visible (+0,20 % / −0,10 %).

### 3. Tabla de 7 bloques de 1 hora
Columnas: Bloque · Sesgo · Var. del bloque · Nivel al final del bloque · Factor dominante (1 frase).

### 4. Veredicto del día
- Sesgo global (alcista / bajista / lateral) y **cierre estimado** (puntos y % frente al cierre anterior).
- **Máximo y mínimo estimados** de la sesión, con el tramo horario de cada uno.
- Tramo de mayor riesgo y tramo de mejor oportunidad.
- Niveles clave: 2 soportes y 2 resistencias.
- **Escenario alternativo**: qué dato o nivel invalidaría la previsión y cómo cambiaría el recorrido (p. ej., "si Michigan sale por encima de X y el bono baja de Y %, …").

### 5. Contexto macro
Resumen en viñetas, con cifra y fuente, de los bloques B–G del Paso 1: Asia, Europa, renta fija, petróleo, calendario, empresas/IA y rotación.

### 6. Fuentes
Lista de las fuentes consultadas, con la hora del dato.

### 7. Aviso legal (obligatorio, al final)
"Este análisis tiene carácter informativo y educativo. Las previsiones son estimaciones probabilísticas basadas en la información disponible a la hora de su elaboración y no constituyen una recomendación personalizada de inversión. Operar con índices y derivados implica riesgo de pérdida. Rentabilidades pasadas no garantizan rentabilidades futuras."

## CONTROL DE CALIDAD (comprueba antes de entregar)
- [ ] Hay 14 tramos (9:00→16:00 ET) y 7 bloques, y cuadran entre sí.
- [ ] La variación acumulada y los niveles en puntos son aritméticamente coherentes con el cierre anterior.
- [ ] El tramo marcado como máximo/mínimo del día coincide con el nivel más alto/bajo de la tabla.
- [ ] Cada dato citado tiene una fuente y una hora; no hay cifras inventadas.
- [ ] Los eventos de calendario aparecen en el tramo horario correcto (hora de Nueva York, ET).
- [ ] El recorrido total es realista según el ATR y la volatilidad (VXN).
- [ ] Incluye el escenario alternativo y el aviso legal.

## VARIABLES
- `{{FECHA}}`: p. ej., 9 de octubre de 2026
- `{{DÍA DE LA SEMANA}}`: p. ej., VIERNES
- (Opcional) `{{NOTAS DEL ANALISTA}}`: noticias o sesgo propio a tener en cuenta.
