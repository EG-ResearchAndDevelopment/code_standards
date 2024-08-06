# Output convention
This repo contains output conventions for various project types. They aim to provide a consistent and readable format for code output.

---

## Table of Contents

1. [Time series analysis](#time-series-analysis)

---

## Time series analysis

Infference of a time series model should be presented in the following format:

| edge_datetime | target_datetime | value | othr ... |
|:-------------:|:---------------:|:-----:|:--------:|
|       1       |        1        | 0.001 |    ...   |
|       1       |        2        | 0.231 |    ...   |
|       1       |        3        | 0.002 |    ...   |
|       1       |        4        | 0.150 |    ...   |
|       2       |        1        | 0.076 |    ...   |
|       2       |        2        | 0.352 |    ...   |
|      ...      |       ...       |  ...  |    ...   |

Where:
- `edge_datetime` is the datetime of the edge data in the batch.
- `target_datetime` is the datetime for which the prediction is made.
- `value` is the predicted value for the target datetime, this can also be a different data type.
- `othr ...` are other columns that may be included in the output.

From the pandas dataframe, the output should be saved in a dictionary format such as json with `pandas.DataFrame.to_dict(orient="list")` method:

```python
df = pd.DataFrame({
    "edge_datetime": [1, 1, 1, 1, 2, 2],
    "target_datetime": [1, 2, 3, 4, 1, 2],
    "value": [0.001, 0.231, 0.002, 0.150, 0.076, 0.352],
    "othr ...": ["...", "...", "...", "...", "...", "..."]
})

output = df.to_dict(orient="list")
```
output **json**:
```json
{
    "edge_datetime": [1, 1, 1, 1, 2, 2],
    "target_datetime": [1, 2, 3, 4, 1, 2],
    "value": [0.001, 0.231, 0.002, 0.150, 0.076, 0.352],
    "othr ...": ["...", "...", "...", "...", "...", "..."]
}
```