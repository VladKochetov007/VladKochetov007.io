# quick_trade by Vlad Kochetov

This package is needed to optimize and facilitate trading with python. the module provides a convenient API for trading.

#### donate
Donationalerts:

[![button](https://i.ibb.co/MgWmjsY/imgonline-com-ua-Resize-y-Wu-Bc-Rv7-KGALSc-Iw.jpg)](https://www.donationalerts.com/r/vladkochetov007)

BTC: 15PrHJ743z2o7KSToNxpYf79gozatiGH6w

ETH: 0x55aAb07b1436fDA7Bd5f85bF95469D1c6ca49E00

USD Digital: 0x55aAb07b1436fDA7Bd5f85bF95469D1c6ca49E00

# tradyng_sys:
The main file of quick_trade.

## PatternFinder

- A class in which you can test and create trading strategies following these rules:
    - exit from the deal - 2.
    - buy - 1.
    - sell - 0.
    - the output of the strategy function has a list format:
         - [... 1, 1, 1, 0, 0, 1, 1, 1, 2, 2, 2, 0, 0 ...]
-

```
df = yf.download(TICKER, period='5y', interval='1d')
trader = PatternFinder(TICKER, 0, df=df, interval='1d')  #  please, use your df
```
### kalman_filter
A method that returns the closure data to which the kalman filter has been applied N times.
Ret type: pd.DataFrame
```
trader.set_pyplot()
filtered = trader.scipy_filter()
trader.strategy_diff(filtered)
```
### scipy_filter
A method that returns the closure data to which the scipy.signal.savgol_filter filter has been applied.
Ret type: pd.DataFrame
```
trader.set_pyplot()
filtered = trader.kalman_filter()
trader.strategy_diff(filtered)
```
### bull_power
Bull power indicator.
Ret type: np.array
```
filtered = trader.bull_power(900)
trader.strategy_diff(filtered)
```
### tema
Triple exponential moмing averageю.
Ret type: pd.DataFrame
```
filtered = trader.tema(70)
trader.strategy_diff(filtered)
```
### linear_
A function to get linear data from an argument.
Ret type: np.array

### get_stop_take
Converts take profit and stop loss from points to specific numbers.
It uses self.stop_loss, self.open_price, self.take_profit and signal.
Ret type: dict
```
{'stop': stop_loss,
'take': take_profit}
```
### strategy_diff
Strategy based on changing the input data (pd.DataFrame).
Ret type: list of predicts.
```
trader.strategy_diff(trader.df['Close'])
```
### strategy_N_ema / strategy_N_sma
Moving average strategy.


![image](https://i.ibb.co/VDDQYJR/IMG-5583.jpg)

### strategy_macd
MACD strategy. MACD, MACD signal


![image](https://i.ibb.co/s1fLBrG/2020-08-03-18-31-14.png)

### strategy_exp_diff
Strategy_diff from tema of close.

### strategy_rsi
RSI strategy.

<div align="left">
  <img src="https://i.ibb.co/hBvCXtQ/IMG-5588.jpg" width=900">
</div>
and:
<div align="left">
  <img src="https://i.ibb.co/RDvfVZT/IMG-5586.jpg" width=900">
</div>

### strategy_macd_rsi
if macd > 0 and rsi > N : buy.

if macd < 0 and rsi < N : sell.

### strategy_parabolic_SAR
PSAR strategy

### strategy_macd_histogram_diff
Based on MACD histogram.

![image](https://i.ibb.co/8YncjYN/IMG-5590.jpg)

### get_network_regression
A method that creates a neural network for regression.
Based on https://medium.com/@randerson112358/stock-price-prediction-using-python-machine-learning-e82a039ac2bb

### strategy_regression_model
A method that creates a series of neural network predictions from closure data.
After that, the method produces strategy_diff and returns a
tuple of predictions for trading and neural network predictions.
```
TICKER = 'EUR=X'
df = yf.download(TICKER)
trader = PatternFinder(TICKER, 0, df=df, interval='1d')
trader.set_pyplot()
trader.load_model('../model-regression')
trader.strategy_regression_model()
```
or
```
TICKER = 'EUR=X'
df = yf.download(TICKER)
trader = PatternFinder(TICKER, 0, df=df, interval='1d')
trader.set_pyplot()
trader.get_network_regression([df])
trader.strategy_regression_model()
```
### get_trained_network
A method that creates a trained neural network for predictions consisting of buy, sell, exit.
The neural network receives data from ta.add_all_ta_features (my_df, fill_na = True).


!> trading predictions are based on the Kalman filter that smoothes the data.


```
TICKER = 'EUR=X'
df = yf.download(TICKER)
trader = PatternFinder(TICKER, 0, df=df, interval='1d')
trader.set_pyplot()
trader.get_trained_network([df])
trader.strategy_with_network()
```
### strategy_with_network
Strategy using a neural network made by the get_trained_network method.

### inverse_strategy
Inverts signals in self.returns.
- buy - sell
- sell - buy
- exit - exit

### basic_backtest
Makes a backtest of the strategy, taking into account your parameters.
Returns pd.DataFrame with all metadata.
The console displays data containing information about the deposit.

### set_pyplot
To set plotly subplots 2x1

### strategy_collider
Colliding 2 strategies.
standard mode:

```
[1, 1, 1, 1, 1, 1, 0, 0, 0, 0, 2, 2, 2, 2, 2, 2, 2, 1, 1, 1, 1, 1, 1, 0, 0, 0, 1, 1, 2, 2, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 1, 2]
[2, 2, 2, 2, 2, 2, 2, 2, 1, 1, 1, 1, 1, 1, 0, 0, 1, 0, 1, 0, 0, 0, 2, 2, 2, 2, 2, 2, 0, 0, 0, 0, 0, 0, 1, 1, 1, 1, 2, 2, 2, 2, 2, 2, 0, 0, 0]
                                                                  to this
[2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 1, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 0, 0, 0, 0, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2]
```
maximalist mode:

```
[1, 1, 1, 1, 1, 1, 0, 0, 0, 0, 2, 2, 2, 2, 2, 2, 2, 1, 1, 1, 1, 1, 1, 0, 0, 0, 1, 1, 2, 2, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 1, 2]
[2, 2, 2, 2, 2, 2, 2, 2, 1, 1, 1, 1, 1, 1, 0, 0, 1, 0, 1, 0, 0, 0, 2, 2, 2, 2, 2, 2, 0, 0, 0, 0, 0, 0, 1, 1, 1, 1, 2, 2, 2, 2, 2, 2, 0, 0, 0]
                                                                  to this
[2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
```
super mode:
```
[1, 1, 1, 1, 1, 1, 0, 0, 0, 0, 2, 2, 2, 2, 2, 2, 2, 1, 1, 1, 1, 1, 1, 0, 0, 0, 1, 1, 2, 2, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 1, 2]
[2, 2, 2, 2, 2, 2, 2, 2, 1, 1, 1, 1, 1, 1, 0, 0, 1, 0, 1, 0, 0, 0, 2, 2, 2, 2, 2, 2, 0, 0, 0, 0, 0, 0, 1, 1, 1, 1, 2, 2, 2, 2, 2, 2, 0, 0, 0]
                                                                  to this
[2, 2, 2, 2, 2, 2, 0, 0, 1, 1, 2, 2, 2, 2, 0, 0, 1, 2, 1, 0, 0, 0, 2, 0, 0, 0, 1, 1, 2, 2, 0, 0, 0, 0, 1, 1, 1, 1, 2, 2, 2, 2, 2, 2, 2, 2, 2]
```
example of the code:
```
TICKER = 'EUR=X'
df = yf.download(TICKER)
trader = PatternFinder(TICKER, 0, df=df, interval='1d')
trader.set_pyplot()
trader.returns = [1,1,1,1,1,1,0,0,0,0,2,2,2,2,2,2,2,1,1,1,1,1,1,0,0,0,1,1,2,2,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,1,2]
ret2 = [2,2,2,2,2,2,2,2,1,1,1,1,1,1,0,0,1,0,1,0,0,0,2,2,2,2,2,2,0,0,0,0,0,0,1,1,1,1,2,2,2,2,2,2,0,0,0]
trader.strategy_collider(args_first_func=(trader.returns,), args_second_func=(ret2,), mode='super')
```

### get_trading_predict
Getting the trading predict based on current returns

### realtime_trading
To trading on real-time.

### log_deposit / log_data
Log X-axis on data/deposit

### backtest
Similar to a backtest, but a candlestick deposit.

### load_model
Loading model from path.

### prepare_scaler
If you are using a loaded neural network,
you need to prepare a scaler suitable for the perception of the neural network.

### find_N
Strategy using trading patterns

# utils:
### set_
This function performs an operation on the data, in which:
if the element is equal to the previous one, then it becomes np.nan.
```
[2, 2, 2, 2, 2, 2, 2, 2, 1, 1, 1, 1, 1, 1, 0, 0, 1, 0, 1, 0, 0, 0, 2, 2, 2, 2, 2, 2, 0, 0, 0, 0, 0, 0, 1, 1, 1, 1, 2, 2, 2, 2, 2, 2, 0, 0, 0]
                                                                  to this
[2, nan, nan, nan, nan, nan, nan, nan, 1, nan, nan, nan, nan, nan, 0, nan, 1, 0, 1, 0, nan, nan, 2, nan, nan, nan, nan, nan, 0, nan, nan, nan, nan, nan, 1, nan, nan, nan, 2, nan, nan, nan, nan, nan, 0, nan, nan]
```
### to_4_col_df
Сonverts list to pd.DataFrame
```
to_4_col_df([1,2,3,4,5,6,7,8,9,10,11,12], 'a', 'b', 'c', 'd')
                        to this
                (pd.DataFrame)
                     a   b   c   d

                0    1   2   3   4
                1    5   6   7   8
                2    9  10  11  12
```
### get_data
Getting IEX minutely data. Sometimes doesn't work.

### anti_set_
opposite of set_

### digit
Splits the data into 3 categories:
- 0
- greater than zero
- less than zero

### get_window
```
>>> get_window([1,2,3,4,5,6,7,8,9], 3)
<<< [[1,2,3],
     [2,3,4],
     [3,4,5],
     [4,5,6]
     [5,6,7],
     [6,7,8],
     [7,8,9]]
```

### inverse_4_col_df
```
>>> inverse_4_col_df(to_4_col_df([1,2,3,4,5,6,7,8,9,10,11,12], *'abcd'), 'a')
<<<      a
    0    1
    1    2
    2    3
    3    4
    4    5
    5    6
    6    7
    7    8
    8    9
    9   10
    10  11
    11  12
```

```
>>> inverse_4_col_df(to_4_col_df([1,2,3,4,5,6,7,8,9,10,11,12], *'abcd'), 'cdf')
<<<      c   d   f
    0    1   1   1
    1    2   2   2
    2    3   3   3
    3    4   4   4
    4    5   5   5
    5    6   6   6
    6    7   7   7
    7    8   8   8
    8    9   9   9
    9   10  10  10
    10  11  11  11
    11  12  12  12
```