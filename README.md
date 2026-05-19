# Crypto Trading Platform

Modular algorithmic trading platform for cryptocurrency markets, extracted from the trading_system scaffold.

## Overview

This is a production-oriented modular scaffold for algorithmic trading and research with explicit risk and approvals. Originally designed for Coinbase Advanced Trade, it's been adapted for broader crypto market use.

## Architecture

```
crypto-trading/
├── apps/                    # Runtime entrypoints
│   ├── api/                 # FastAPI trading API
│   ├── backtester/          # Backtesting engine
│   ├── paper_exchange/      # Paper trading simulator
│   ├── replay_engine/       # Market data replay
│   └── worker/              # Background worker processes
├── core/                    # Core trading subsystems
│   ├── config/              # Configuration management
│   ├── events/              # Event system
│   ├── logging/             # Structured logging
│   ├── models/              # Domain models
│   ├── security/            # Security utilities
│   └── utils/               # Common utilities
├── exchange/                # Exchange integrations
│   └── coinbase/            # Coinbase Advanced Trade
├── execution/               # Order management
│   ├── hybrid/              # Hybrid CEX/onchain execution
│   ├── maker_engine/        # Market making engine
│   ├── order_manager/       # Order lifecycle
│   ├── queue_model/         # Order queue modeling
│   ├── router/              # Smart order routing
│   ├── smart_execution/     # Execution algorithms
│   └── trade_lifecycle/     # Trade tracking
├── market_data/             # Market data processing
│   ├── candles/             # OHLCV data
│   ├── features/            # Feature engineering
│   ├── indicators/          # Technical indicators
│   ├── microstructure/      # Orderbook analysis
│   ├── orderbook/           # Orderbook management
│   ├── storage/             # Data storage
│   └── trades/              # Trade data
├── onchain/                 # Onchain trading modules
│   ├── bridges/             # Cross-chain bridges
│   ├── chains/              # Blockchain support
│   ├── contracts/           # Smart contract interaction
│   ├── data/                # Onchain data sources
│   ├── dex/                 # DEX integrations
│   ├── mev_protection/      # MEV protection
│   ├── security/            # Contract security
│   ├── simulation/          # Onchain simulation
│   ├── strategies/          # Onchain strategies
│   └── wallets/             # Wallet management
├── portfolio/               # Portfolio management
│   ├── allocator/           # Capital allocation
│   ├── capital_buckets/     # Liquidity management
│   ├── liquidity_distribution/
│   ├── objectives/          # Portfolio objectives
│   ├── performance/         # Performance tracking
│   └── rebalance/           # Rebalancing logic
├── research/                # Research tools
│   ├── experiment_tracking/
│   └── lp/                  # Liquidity provider research
├── risk/                    # Risk management
│   ├── approvals/           # Approval workflows
│   ├── compliance/          # Compliance checks
│   ├── drawdown/            # Drawdown monitoring
│   ├── engine/              # Risk engine
│   ├── kill_switch/         # Emergency shutdown
│   ├── limits/              # Position limits
│   ├── sizing/              # Position sizing
│   └── slippage/            # Slippage analysis
├── strategies/              # Trading strategies
│   ├── accumulation/        # DCA strategies
│   ├── base/                # Strategy interfaces
│   ├── catalog/             # Strategy registry
│   ├── ensemble/            # Multi-strategy ensemble
│   ├── execution_algos/     # VWAP/TWAP algorithms
│   ├── market_making/       # Market making strategies
│   ├── mean_reversion/      # Mean reversion strategies
│   ├── microstructure/      # Microstructure strategies
│   ├── registry/            # Strategy registry
│   ├── special/             # Special strategies
│   ├── stat_arb/            # Statistical arbitrage
│   ├── trend/               # Trend following
│   └── volatility/          # Volatility strategies
├── tests/                   # Test suites
├── docs/                    # Documentation
├── configs/                 # Configuration files
├── scripts/                 # Utility scripts
└── storage/                 # Data storage modules
```

## Quick Start

### Local Setup

```bash
# Install dependencies
pip install -e .[dev]

# Optional: Start local infrastructure
docker compose up -d postgres redis

# Run the API
uvicorn apps.api.main:app --reload --host 0.0.0.0 --port 8000

# Run the worker
python -m apps.worker.main

# Run backtest demo
python -m apps.backtester.runner --config configs/backtest_demo.yaml

# Run replay demo
python -m apps.replay_engine.runner --fixture apps/replay_engine/fixtures/maker_toxic_flow.jsonl
```

### Testing

```bash
# Full local quality gate
make ci

# Or run individually
pytest
```

## Development

### Adding New Strategies

1. Create a new directory under `strategies/`
2. Implement the strategy interface from `strategies/base/interfaces.py`
3. Register in `strategies/registry/registry.py`
4. Add configuration in `configs/`
5. Add tests in `tests/`

### Adding Exchange Support

1. Create a new directory under `exchange/`
2. Implement the exchange interface
3. Add authentication and execution methods
4. Add tests for the exchange integration

### Adding Onchain Strategies

1. Create a new directory under `onchain/strategies/`
2. Implement the strategy interface
3. Add contract interactions in `onchain/contracts/`
4. Add simulation in `onchain/simulation/`
5. Add tests in `tests/`

## Configuration

Configuration files are in the `configs/` directory:

- `configs/local_dev.yaml` - Local development settings
- `configs/paper_mode.yaml` - Paper trading settings
- `configs/live_approval_mode.yaml` - Live trading with approval
- `configs/onchain_mm/` - Onchain market making configs
- `configs/accumulation_mode.yaml` - DCA strategy config
- `configs/market_making_mode.yaml` - Market making config
- `configs/trend_mode.yaml` - Trend following config
- `configs/mean_reversion_mode.yaml` - Mean reversion config

## Risk Management

The platform includes comprehensive risk management:

- **Kill Switch**: Emergency shutdown mechanism
- **Position Limits**: Maximum position sizes
- **Drawdown Monitoring**: Real-time drawdown tracking
- **Slippage Analysis**: Execution quality monitoring
- **Compliance Checks**: Regulatory compliance
- **Approval Workflows**: Multi-level approval for live trading

## Future Development

### Trade Analysis Features

- Real-time P&L tracking
- Strategy performance attribution
- Risk metrics calculation
- Market regime detection
- Correlation analysis

### Trade Execution Features

- Smart order routing
- Execution quality analysis
- Market impact modeling
- Cross-exchange arbitrage
- Onchain/CEX hybrid execution

### Monitoring and Alerts

- Real-time dashboard
- Performance alerts
- Risk threshold alerts
- System health monitoring
- Trade execution alerts

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests
5. Submit a pull request

## License

This project is proprietary and confidential.

## Contact

For questions or support, contact the development team.
