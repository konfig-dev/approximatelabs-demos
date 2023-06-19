# sketch.howto

Interactive demo for `sketch.howto`

### Import data

In this demo we will import sales data with PII information.

:::form

```python
import sketch
import pandas as pd
pd.set_option('display.max_columns', None)
sales_data = pd.read_csv("https://gist.githubusercontent.com/bluecoconut/9ce2135aafb5c6ab2dc1d60ac595646e/raw/c93c3500a1f7fae469cba716f09358cfddea6343/sales_demo_with_pii_and_all_states.csv")
sales_data.head(10)
```

::button[Import Data]

:::

### howto

`howto` is the basic "code-writing" prompt in sketch. This will return a
code-block you should be able to copy paste and use as a starting point (or
possibly ending!) for any question you have to ask of the data. Ask this how to
clean the data, normalize, create new features, plot, and even build models!

:::form

::input{name=QUERY label=Query description="Ask sketch how to do anythign the dataframe"}

```python
answer = sales_data.sketch.howto(QUERY, call_display=False)
print(QUERY, answer)
```

::button[Howto]

:::
