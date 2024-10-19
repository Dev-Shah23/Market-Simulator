# Stock Price Chart API

This Flask application fetches historical and intraday stock data from Yahoo Finance using `yfinance`, identifies price peaks, and generates a chart with matplotlib. The chart and data, including current stock price and percentage change, are provided via API responses.

## Features
- Fetch historical and intraday stock price data for any symbol available on Yahoo Finance.
- Identify peaks in historical stock prices.
- Generate a stock price chart that includes both historical and intraday data.
- Return current stock price, price change, and percentage change.
- API to retrieve chart and stock data in JSON format.

## Requirements

- Python 3.x
- Flask
- yfinance
- pandas
- numpy
- matplotlib

## Installation

1. **Clone the repository**:
   ```bash
   git clone https://github.com/yourusername/stock-chart-api.git
   cd Market-Simulator
   ```

2. **Create and activate a virtual environment** (optional but recommended):
   ```bash
   python3 -m venv venv
   source venv/bin/activate
   ```

3. **Install the dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

4. **Run the application**:
   ```bash
   python app.py
   ```

## API Usage

### 1. Fetch Stock Chart and Data
Fetches intraday and historical data, generates a stock price chart, and returns the stock price information.

**Endpoint**: `/fetch-stock-chart`  
**Method**: `GET`

#### Query Parameters:
- `symbol` (required): The stock symbol (e.g., `AAPL`, `TSLA`).
- `period` (required): The historical period to consider (e.g., `1 week`, `1 month`, `1 year`).

#### Example:
```bash
GET /fetch-stock-chart?symbol=TSLA&period=1 week
```

#### Response:
```json
{
  "current_price": 780.45,
  "price_change": 12.34,
  "percentage_change": 1.60,
  "image_url": "/tmp/tmpabc123.png"
}
```

- `current_price`: The current stock price.
- `price_change`: The difference from the previous closing price.
- `percentage_change`: The percentage change compared to the previous closing price.
- `image_url`: Path to the generated stock chart image.

### 2. Error Responses:
- **400 Bad Request**: Invalid input such as missing or malformed query parameters.
- **404 Not Found**: No stock data found for the provided symbol.
- **500 Internal Server Error**: An unexpected server error occurred.

## Project Structure

```bash
.
├── app.py                  # Main Flask app
├── requirements.txt        # List of dependencies
└── README.md               # Project documentation
```

## How It Works

1. **Fetching Data**:  
   The app uses `yfinance` to fetch historical stock data and live intraday data. The intraday data is updated every minute.

2. **Identifying Peaks**:  
   Peaks in the historical data are identified using a simple NumPy method that compares neighboring data points.

3. **Generating Charts**:  
   Using `matplotlib`, the app generates a chart that visualizes historical and intraday stock data. Peaks in the historical data are highlighted with scatter points.

4. **Returning Data**:  
   The app returns stock information (current price, change, etc.) along with a dynamically generated chart as part of the API response.

## Logging
The app uses Python's built-in `logging` module to handle logging at the `INFO` level. Verbose logs from `matplotlib` and other noisy libraries are suppressed to keep the logs clean.

## Future Enhancements
- Support for additional stock data metrics (e.g., volume, moving averages).
- Add caching to reduce repeated requests for the same data.
- Integrate with a database to store historical requests and responses.

## License
This project is licensed under the MIT License.

---

This `README.md` provides an overview of the project, its API usage, and instructions for installation and running.
