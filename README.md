# Volatility Surface Anomaly Detection & Trading System

## Technical Architecture

### Core Components
- **Data Pipeline**: yfinance API for options chain retrieval (15-120 DTE configurable)
- **Volatility Surface Construction**: Black-Scholes with dividend adjustment (5.00%), surface smoothing via SciPy
- **Anomaly Detection**: Convolutional autoencoder trained on simulated surfaces with varying skew/smile parameters
- **Market Regime Classification**: Four-state model (low volatility, normal, high volatility, crisis) based on VIX percentile, term structure slope, and skew steepness
- **Strategy Generator**: Rules-based recommendations linked to detected anomaly location and market regime

### ML Implementation
- Tensorflow/Keras implementation
- Reconstruction error threshold: 0.0000 (configurable)
- Model architecture: 3 convolutional layers (encoder), 3 transposed convolutional layers (decoder)
- Loss function: MSE with L1 regularization
- Training data: 10,000+ synthetic surfaces with parametric variations

### Anomaly Quantification
- Anomaly score calculation: normalized reconstruction error
- Localization via gradient-based saliency mapping
- Moneyness/maturity coordinates with maximum deviation identified programmatically
- Magnitude measured as volatility point difference from expected surface

### Visualization Modules
- Heatmap representation with anomaly highlighting
- 3D surface with interactive rotation (Plotly)
- Term structure across moneyness levels
- Skew visualization across maturities
- Strategy payoff diagram with breakeven markers
