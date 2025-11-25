# tata-motors-stock-analysis
This repository features minute-level Tata Motors (NSE) trading data with technical indicators and sentiment scores. Includes EDA, SQL queries, and ML-ready preprocessing for stock trend analysis, algorithmic trading, and forecasting models.

**Tata Motors Stock Analysis Dataset (Minute-Level, Technical Indicators, Sentiment)**
This project provides a complete, minute-level dataset for Tata Motors Limited (NSE: TATAMOTORS) enriched with technical indicators, volume analytics, and sentiment-derived metrics. It is designed for quantitative research, algorithmic trading, and machine learning–based stock forecasting.
________________________________________     
**Problem Statement**
Financial markets generate vast amounts of data every minute. Traders and analysts often struggle to extract meaningful insights from noisy intraday fluctuations. Predicting short-term price movements is especially challenging due to rapid volatility and the interdependence of technical indicators.
This project aims to solve that challenge by creating a structured, high-frequency dataset that integrates: 
•	Historical intraday price movements
•	Widely-used technical analysis indicators
•	Volume-based analytics
•	Sentiment scores from financial news
The goal is to support algorithmic trading, quantitative finance, technical analysis, and machine learning forecasting models by offering a comprehensive feature-rich dataset for research and real-world applications.
________________________________________
**Project Summary**
This repository contains a structured dataset that captures:
•	Minute-by-minute OHLC price data
•	Technical indicators such as:
o	RSI
o	MACD (12-26-9)
o	MACD Histogram
o	EMA (20/50/100)
o	SMA (20/50)
•	Volume features
o	10-day average volume
o	50-day average volume
o	volume ratio
o	intraday volume surges
•	Market sentiment score
•	52-week high tracking
•	Combined Master Technical Score for trading decision support
This dataset enables traders and ML practitioners to build powerful intraday forecasting, volatility prediction, pattern detection, and backtesting systems.
________________________________________
**Dataset Schema**
Below is the structure of the dataset:
+----------------------+-----------------------------+
| Column Name          | Description                 |
+----------------------+-----------------------------+
| timestamp            | Minute-level timestamp      |
| open                 | Opening price               |
| high                 | Highest price               |
| low                  | Lowest price                |
| close                | Closing price               |
| volume               | Trade volume                |
| RSI                  | Relative Strength Index     |
| MACD_12_26_9         | MACD line                   |
| MACDs_12_26_9        | MACD Signal line            |
| MACDh_12_26_9        | MACD Histogram              |
| avg_volume_10d       | 10-day average volume       |
| avg_volume_50d       | 50-day average volume       |
| volume_ratio         | Volume spike indicator      |
| master_score         | Combined technical score    |
| 52_week_high         | Highest price in 52 weeks   |
| distance_from_high   | % distance from 52W high    |
| sentiment_score      | News sentiment score        |
+----------------------+-----------------------------+
Dataset file used:
📁 /mnt/data/final_dataset_tata_motors.csv
________________________________________
**Use Cases**
This dataset is ideal for:
✔ Algorithmic Trading
Generate buy/sell signals using technical indicators.
✔ Technical Analysis
Study market momentum, trend reversals, overbought/oversold conditions.
✔ Machine Learning Models
Build:
•	price direction classifiers
•	LSTM forecasting models
•	volatility prediction models
•	ensemble-based strategies
✔ Quantitative Research
Research intraday market behavior and microtrends.
________________________________________
**Example SQL Queries**
1. Daily OHLC Summary
SELECT 
    DATE(timestamp) AS trade_date,
    MIN(open) AS open_price,
    MAX(high) AS high_price,
    MIN(low) AS low_price,
    MAX(close) AS close_price
FROM stock_data
GROUP BY DATE(timestamp);
2. Overbought Zone Detection (RSI > 70)
SELECT timestamp, close, RSI
FROM stock_data
WHERE RSI > 70;

3. Bullish MACD Crossover
SELECT timestamp, MACD_12_26_9, MACDs_12_26_9
FROM stock_data
WHERE MACD_12_26_9 > MACDs_12_26_9;
4. High Volume Price Surge (>1%)
SELECT timestamp, open, close, volume
FROM stock_data
WHERE ((close - open) / open) * 100 > 1
  AND volume > avg_volume_10d;
5. Close to 52-Week High
SELECT timestamp, close, 52_week_high, distance_from_high
FROM stock_data
WHERE distance_from_high < 2;
6. Trend Reversal (MACD Histogram Flip)
SELECT 
    timestamp,
    MACDh_12_26_9,
    LAG(MACDh_12_26_9) OVER (ORDER BY timestamp) AS prev_hist
FROM stock_data
WHERE SIGN(MACDh_12_26_9) != SIGN(LAG(MACDh_12_26_9) OVER (ORDER BY timestamp));
________________________________________
 **Example Visualizations** 
•	RSI over time
•	MACD crossover chart
•	Volume spikes
•	Price vs EMA trend
•	Sentiment vs price movement
________________________________________
**Conclusion**
This project provides a comprehensive dataset combining intraday price movements, technical analysis features, volume-based metrics, and market sentiment. It serves as a strong foundation for:
•	Machine learning forecasting
•	Algorithmic trading model design
•	Quantitative financial research
•	High-frequency trend and signal analysis
By integrating multiple financial indicators into a single dataset, this project bridges the gap between raw market data and actionable trading signals.


