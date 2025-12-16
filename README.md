# Volume-Price-Phase-Shift-VPPS
The Volume-Price Phase Shift (VPPS) indicator measures the relative divergence between price momentum and volume momentum.

# Overview

Volume-Price Phase Shift (VPPS) is a regime-aware oscillator designed to measure the temporal relationship between volume impulses and price impulses.

Rather than asking whether volume confirms price, VPPS asks a more precise question:

Does volume lead price, or does price move ahead of volume?

This distinction is critical for identifying accumulation, distribution, breakout quality, trend exhaustion, and false price moves that lack participation.

VPPS is normalized, volatility-adjusted, statistically expanded, and intended to be displayed in its own panel.

# Conceptual Foundation

Markets move through impulses, not continuous flows.
Each impulse has both a price component and a volume component.

Four recurring regimes exist:

1. Volume leads price (accumulation / distribution)
2. Volume and price move together (sustainable trend)
3. Price leads volume (weak or speculative moves)
4. Neither leads (noise or compression)

VPPS measures which impulse arrives first.

# Mathematical Construction

VPPS is built in layered stages to isolate and normalize informational dominance.

1. Impulse Extraction

   We analyze changes rather than absolute values:

   $\Delta P_t = Close_t − Close_{t-1}$

   $\Delta V_t = Volume_t − Volume_{t-1}$

3. Phase Smoothing

   Both impulses are smoothed to extract their dominant phase:

   $P_t = EMA(\Delta P_t, n)$

   $V_t = EMA(\Delta V_t, n)$

   This approximates the directional phase of price and volume impulses.

3. Volatility and Scale Normalization

   Price impulses are normalized by volatility:

   $P^*_t = \frac{P_t}{ATR_n}$

   Volume impulses are normalized by average traded volume:

   $V^*_t = \frac{V_t}{SMA(Volume, n)}$

   This ensures consistent behavior across assets and timeframes.

5. Phase Shift Calculation

   The core signal is the difference between normalized impulses:

   $VPPS_{raw_t} = P^* _t − V^* _t$

   Interpretation:

   * Positive values indicate price leading volume
   * Negative values indicate volume leading price

5. Adaptive Statistical Expansion

   Smoothing and normalization naturally compress signal amplitude.

   To restore meaningful dynamic range without arbitrary scaling, VPPS applies Z-score expansion:

   $Z_t = \frac{(VPPS_{raw_t} − μ)}{σ}$

   Where:

   * $μ$ is the rolling mean of VPPS_raw
   * $σ$ is the rolling standard deviation

   This makes VPPS self-normalizing and regime-adaptive.

6. Soft Saturation and Scaling

   To prevent instability while preserving extremes, a soft saturation function is applied:

   $S_t = \frac{Z_t \cdot g}{1 + |Z_t \cdot g|}$

   The final oscillator is mapped to a 0–100 scale:

   $VPPS_t = 50 + 50 · S_t$

   Values may exceed this range during extreme conditions.

# Interpretation

VPPS is a phase-lead oscillator, not a momentum or volume-strength indicator.

# Zone Interpretation

VPPS > 80:      Price significantly leading volume — potential exhaustion or weak continuation

VPPS 50–80:      Price slightly ahead of volume

VPPS 20–50:      Volume leading price — constructive participation

VPPS < 20:      Strong accumulation or distribution

# Key Behavioral Insights

   * Low VPPS before breakouts suggests higher probability of follow-through
   * Rising VPPS during trends indicates weakening participation
   * Falling VPPS in ranges often signals stealth accumulation
   * Persistent extremes reflect regime imbalance

VPPS is most effective as a context filter, not a standalone signal generator.

# What VPPS Is Not

VPPS is not:

On-Balance Volume (OBV)

   * A volume oscillator
   * A correlation metric
   * A momentum indicator

It does not measure how much volume traded.

It measures when volume acted relative to price.

# Practical Use Cases

   * Breakout validation
   * Accumulation and distribution detection
   * Trend exhaustion analysis
   * Regime filtering for momentum systems

VPPS is designed to complement price-based indicators, not replace them.

# Design Principles

   * Volatility-aware
   * Asset-agnostic
   * Regime-sensitive
   * Information-theoretic rather than price-centric

