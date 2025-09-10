# MT5 Trading Connector

A comprehensive Python-based trading system that connects to MetaTrader 5 (MT5) terminal for automated trading operations, data synchronization, and technical analysis.

![SMC Indicator Screenshot 1](image_1.png)

## 🚀 Features

- **Real-time Trading**: Place buy/sell orders with automatic lot size calculation based on risk management
- **Data Synchronization**: Automated sync of candle data, trades, and trade requests to MongoDB
- **Technical Indicators**: Built-in support for SMA, EMA, RSI, ATR, and Volume indicators
- **Risk Management**: Configurable risk percentage and lot size limits
- **RESTful API**: Flask-based API for external trading operations
- **Scheduled Jobs**: Background tasks for data synchronization and maintenance
- **Multi-timeframe Support**: M1, M15, and H4 timeframes for various currency pairs

## 📋 Prerequisites

- Python 3.8+
- MetaTrader 5 terminal installed and running
- MongoDB database (local or cloud)
- Active trading account with MT5 broker

## 🛠️ Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd mt5-connector
   ```

2. **Create a virtual environment**
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Configure environment variables**
   ```bash
   export API_KEY="your_api_key_here"  # Optional: defaults to "lesely_key"
   ```

5. **Set up MongoDB**
   - Install MongoDB locally or use MongoDB Atlas
   - Update connection string in `app/services/mongo_service.py` if needed

## ⚙️ Configuration

### API Configuration
Edit `config.py` to customize:
- `SECRET_KEY`: Flask secret key
- `DEBUG`: Enable/disable debug mode
- `API_KEY`: API authentication key

### Database Configuration
Update `app/services/mongo_service.py`:
```python
# For local MongoDB
url = "mongodb://localhost:27017/"

# For MongoDB Atlas
url = "mongodb+srv://username:password@cluster.mongodb.net/"
```

## 🚀 Usage

### Starting the Application
```bash
python run.py
```

The application will start on `http://localhost:5000` with the following features:
- Automatic data synchronization every minute/hour
- Background job scheduling for trades and candles
- RESTful API endpoints for trading operations

### API Endpoints

#### Trading Operations
- `POST /place_order` - Place a new trading order
  ```json
  {
    "currencyPair": "EURUSD",
    "entryPrice": 1.1000,
    "stopLevelPrice": 1.0950,
    "profitLevelPrice": 1.1100,
    "stopLevelTicks": 50,
    "profitLevelTicks": 100,
    "risk": 0.5
  }
  ```

#### Data Retrieval
- `GET /candles` - Get candle data for a specific time range
  ```
  /candles?start_time=2024-01-01T00:00:00&end_time=2024-01-02T00:00:00&currency_pair=EURUSD&time_frame=m1
  ```
- `GET /closed_trades` - Get all closed trades
- `GET /trade-request/<order_id>` - Get specific trade request details

### Supported Currency Pairs
- XAUUSD (Gold)
- EURUSD
- GBPUSD
- AUDUSD
- USDCAD

### Supported Timeframes
- M1 (1 minute)
- M15 (15 minutes)
- H4 (4 hours)

## 📊 Technical Indicators

The system automatically calculates and stores the following indicators:

- **SMA (Simple Moving Average)**: 14-period
- **EMA (Exponential Moving Average)**: 14-period
- **RSI (Relative Strength Index)**: 14-period
- **ATR (Average True Range)**: 14-period
- **Volume**: Total volume over specified periods

## 🔧 Project Structure

```
mt5-connector/
├── app/
│   ├── indicators/          # Technical indicator calculations
│   ├── jobs/               # Background synchronization jobs
│   ├── modals/             # Database models and schemas
│   ├── routes/             # Flask API routes
│   ├── services/           # Core business logic
│   ├── templates/          # HTML templates
│   └── utils/              # Utility functions
├── tests/                  # Unit tests
├── config.py              # Application configuration
├── requirements.txt       # Python dependencies
└── run.py                # Application entry point
```

## 🔒 Security

- API key authentication for trading endpoints
- Risk management limits (max 1% risk per trade)
- Lot size limits (max 5 lots, max 3 lots for XAUUSD)
- Rate limiting for order placement (10-second cooldown)

## 📈 Scheduled Jobs

The application runs several background jobs:

- **Trade Sync**: Every 5 minutes - syncs closed trades
- **Candle Sync**: 
  - M1: Every minute
  - M15: Every 15 minutes
  - H4: Every 4 hours

## 🧪 Testing

Run the test suite:
```bash
python -m pytest tests/
```

Or run individual tests:
```bash
python tests/test_routes.py
```

## 📝 Logging

Logs are stored in the `logs/` directory with:
- Rotating file handler (10MB max, 5 backups)
- Console output in debug mode
- Structured logging with timestamps

## 🚨 Error Handling

The application includes comprehensive error handling:
- MT5 connection failures
- Database operation errors
- Invalid trading parameters
- API authentication failures

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests for new functionality
5. Submit a pull request

## 📄 License

Copyright © 2025 LesleyJJ. All rights reserved.

## ⚠️ Disclaimer

This software is for educational and research purposes only. Trading involves substantial risk of loss and is not suitable for all investors. Past performance is not indicative of future results. Always test thoroughly in a demo environment before using with real funds.

## 🆘 Support

For issues and questions:
1. Check the logs in the `logs/` directory
2. Verify MT5 terminal is running and connected
3. Ensure MongoDB is accessible
4. Review API key configuration

## 🔄 Version History

- **v1.0.0**: Initial release with basic trading functionality
- Core features: Order placement, data sync, technical indicators

---

**Note:** The full source code is not publicly available. If you are interested in accessing the source code or collaborating, please  [contact me](mailto:jacobjohnlesley@gmail.com).