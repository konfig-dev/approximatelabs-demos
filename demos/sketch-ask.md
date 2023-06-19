# sketch.ask

Interactive demo for `sketch.ask`

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

### ask

`ask` is a basic question-answer system on sketch, this will return an answer in
text that is based off of the summary statistics and description of the data.

:::form

::input{name=QUERY label=Query description="Ask sketch anything about the dataframe"}

```python
answer = sales_data.sketch.ask(QUERY, call_display=False)
print(QUERY, answer)
```

::button[Ask]

:::
