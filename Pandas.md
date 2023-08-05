Pandas is a library used extensively to read .csv files and make dataframes to process large amounts of data quickly and seamlessly

#### Usecase:

```python
import pandas as pd

data = pd.read_csv('Path\Data.csv')

column = data["column"] #Get a specific column
row = data[data["id"] == value] #Get a specific row

multiple_keys = data[(data["id"] == value) & (data["column"] == value)]["column"] #Multiple condition chaining

list_values = data["column"].tolist()
unique = data["column"].unique()

```