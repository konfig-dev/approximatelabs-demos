# Sketch Demo

:a[Sketch]{target=\_blank href=https://github.com/approximatelabs/sketch} is an AI code-writing assistant for pandas users that understands the
context of your data, greatly improving the relevance of suggestions. Sketch is
usable in seconds and doesn't require adding a plugin to your IDE.

The following demo runs through a list of example queries on a Pandas dataframe using Sketch.
and then allows you to try your own inputs.

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

### sketch.ask

Ask is a basic question-answer system on sketch, this will return an answer in
text that is based off of the summary statistics and description of the data.

Use ask to get an understanding of the data, get better column names, ask
hypotheticals (how would I go about doing X with this data), and more.

:::form

```python
query = "What columns might have PII information in them?"
answer = sales_data.sketch.ask(query, call_display=False)
print(query, answer)
```

::button[Ask]

:::

### sketch.ask [list]

:::form

```python
query = "Can you give me friendly names for each column? (output as an HTML list)"
sales_data.sketch.ask(query)
answer = sales_data.sketch.ask(query, call_display=False)
print(query, answer)
```

::button[Ask]

:::

### sketch.howto [write]

:::form

```python
query = "Create some derived features from the address"
code = sales_data.sketch.howto(query, call_display=False)
print(query, code)
```

::button[Howto]

:::

### Run generated code from "Create some derived features from the address"

:::form

```python
# Create a new column for the city
sales_data['City'] = sales_data['Purchase Address'].apply(lambda x: x.split(',')[1])

# Create a new column for the state
sales_data['State'] = sales_data['Purchase Address'].apply(lambda x: x.split(',')[2].split(' ')[1])

# Create a new column for the zipcode
sales_data['Zipcode'] = sales_data['Purchase Address'].apply(lambda x: x.split(',')[2].split(' ')[2])

sales_data[["Purchase Address", "City", "State", "Zipcode"]]
```

::button[Run]

:::

### sketch.howto [read]

Howto is the basic "code-writing" prompt in sketch. This will return a
code-block you should be able to copy paste and use as a starting point (or
possibly ending!) for any question you have to ask of the data. Ask this how to
clean the data, normalize, create new features, plot, and even build models!

:::form

```python
query = "Get the top 5 grossing states"
code = sales_data.sketch.howto(query, call_display=False)
print(query, code)
```

::button[Howto]

:::

### Run generated code from "Get the top 5 grossing states"

:::form

```python
# Get the top 5 grossing states

# Calculate total sales per state
state_sales = sales_data.groupby('State')['Price Each'].sum().reset_index()

# Sort the dataframe by total sales in descending order
state_sales = state_sales.sort_values(by='Price Each', ascending=False)

# Get the top 5 grossing states
top_5_states = state_sales.head(5)

# Print the results
print(top_5_states)
```

::button[Run]

:::
