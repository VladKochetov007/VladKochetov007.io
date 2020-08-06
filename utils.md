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
