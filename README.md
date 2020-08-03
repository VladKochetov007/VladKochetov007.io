
# quick_trade by Vlad Kochetov

this package is needed to optimize and facilitate trading with python. the module provides a convenient API for trading.

#### donate
[![button](https://i.ibb.co/MgWmjsY/imgonline-com-ua-Resize-y-Wu-Bc-Rv7-KGALSc-Iw.jpg)](https://www.donationalerts.com/r/vladkochetov007)

## tradyng_sys:
the main file of quick_trade.

### PatternFinder

- a class in which you can test and create trading strategies following these rules:
    - exit from the deal - 2.
    - buy - 1.
    - sell - 0.
    - the output of the strategy function has a list format:
         - [... 1, 1, 1, 0, 0, 1, 1, 1, 2, 2, 2, 0, 0 ...]
```
df = yf.download(TICKER, period='5y', interval='1d')
trader = PatternFinder(TICKER, 0, df=df, interval='1d')  #  please, use your df
```
#### kalman_filter
a method that returns the closure data to which the kalman filter has been applied N times.
Ret type: pd.DataFrame
```
trader.set_pyplot()
filtered = trader.scipy_filter()
trader.strategy_diff(filtered)
```
#### scipy_filter
a method that returns the closure data to which the scipy.signal.savgol_filter filter has been applied.
Ret type: pd.DataFrame
```
trader.set_pyplot()
filtered = trader.kalman_filter()
trader.strategy_diff(filtered)
```
#### bull_power
bull power indicator.
Ret type: np.array
```
filtered = trader.bull_power(900)
trader.strategy_diff(filtered)
```
#### tema
triple exponential moмing averageю.
Ret type: pd.DataFrame
```
filtered = trader.tema(70)
trader.strategy_diff(filtered)
```
#### linear_
a function to get linear data from an argument.
Ret type: np.array
#### get_stop_take
converts take profit and stop loss from points to specific numbers.
It uses self.stop_loss, self.open_price, self.take_profit.
Ret type: dict
```
{'stop': _stop_loss,
'take': take}
```