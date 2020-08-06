# About
This package is needed to optimize and facilitate trading with python. the module provides a convenient API for trading.

```
used:
 ├──ta by Darío López Padial (Bukosabino   https://github.com/bukosabino/ta)
 ├──tensorflow==2.2 (https://github.com/tensorflow/tensorflow)
 ├──pykalman (https://github.com/pykalman/pykalman)
 ├──tqdm (https://github.com/tqdm/tqdm)
 ├──plotly (https://github.com/plotly/plotly.py)
 ├──scipy (https://github.com/scipy/scipy)
 ├──logging
 ├──pandas (https://github.com/pandas-dev/pandas)
 ├──numpy (https://github.com/numpy/numpy)
 ├──itertools
 ├──datetime
 ├──os
 ├──scipy
 └──iexfinance (https://github.com/addisonlynch/iexfinance)
```


algo-trading system.
trading with python.


## customize your strategy!

```
from quick_trade.trading_sys import PatternFinder
import yfinance as yf

class my_trader(PatternFinder):
    def strategy_buy_and_hold(
            self):
        ret = []
        for i in self.df['Close'].values:
            ret.append(1)
        self.returns = ret
        return ret


a = my_trader('MSFT', df=yf.download('MSFT', start='2019-01-01'))
a.set_pyplot()
a.strategy_buy_and_hold()
a.backtest()
```


- 1 -- Buy

- 2 -- Exit

- 0 -- Sell
