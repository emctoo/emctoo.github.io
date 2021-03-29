#### display all rows and columns

 pandas autodetects the size of your terminal window if you set 

```python
pd.options.display.width = 0
```

```python
pd.set_option('display.max_rows', 500)
pd.set_option('display.max_columns', 1000)
pd.set_option('display.width', 2000)
```



#### [**TODO**] [just panda things](https://github.com/chiphuyen/just-pandas-things/blob/master/just-pandas-things.ipynb) 

pandas 一些出人意料的地方，以及对性能有帮助的小tips。

#### **[TODO]** [fast pandas](https://github.com/mm-mansour/Fast-Pandas)

benchmark pandas

[joyful pandas](https://github.com/yeayee/joyful-pandas)

#### pandas write to excel, with sheets

`pd.ExcelWriter` 可以用不同的engine，比如 [openpyxl](https://openpyxl.readthedocs.io/en/stable/)。

```python
with pd.ExcelWriter('hello.xlsx') as writer:
    df1.to_excel(writer, sheet_name='df1')
    df2.to_excel(writer, sheet_name='df2')
```

写入的时候datetime不能是aware timezone的，可以:

```
my_series.dt.tz_localize(None)
```

