# Sales Prediction with Python

This project predicts sales from advertising spend on TV, Radio and Newspaper. I trained two regression models and compared how well each predicted sales on rows it had not seen before.

- **Linear Regression** is the simple baseline. It assumes each channel adds a fixed amount to sales.
- **Random Forest** combines many decision trees and can capture more complex patterns.

## Dataset

The dataset is `data/Advertising.csv`, with 200 rows.

| Column | Meaning |
|---|---|
| Unnamed: 0 | Row number (removed, not useful for prediction) |
| TV | Advertising spend on TV |
| Radio | Advertising spend on Radio |
| Newspaper | Advertising spend on Newspaper |
| Sales | Sales. This is the value the models predict. |

The dataset has no dates, so I used regression instead of time series forecasting.

## Cleaning and feature selection

1. **Removed the `Unnamed: 0` column**, which is only a row number.
2. **Checked for problems.** There are no missing values and no duplicate rows, so no other cleaning was needed.
3. **Checked the relationships with sales.** TV has the strongest link (correlation 0.78), then Radio (0.58), then Newspaper (0.23).
4. **Kept all three channels as features** so the models could show whether Newspaper adds anything.
5. **Split the data** into 80% for training (160 rows) and 20% for testing (40 rows).

## How to run

1. Keep `Advertising.csv` inside the `data` folder, next to the notebook.
2. Open `sales_prediction.ipynb` in Jupyter Notebook, JupyterLab or Google Colab.
3. Run all cells from top to bottom. The results appear under "Compare the Results".

## Results

| Model | MAE | RMSE | R2 |
|---|---|---|---|
| Linear Regression | 1.46 | 1.78 | 0.90 |
| Random Forest | 0.63 | 0.76 | 0.98 |

**How to read the metrics:**
- **MAE** is the average size of a prediction error. Lower is better.
- **RMSE** is similar to MAE, but large errors count more. Lower is better.
- **R2** is how much of the change in sales the model explains. Closer to 1 is better.

## What the results show

Random Forest performed better on every measure. It explained 98% of the change in sales on the test data, compared with 90% for Linear Regression.

The Linear Regression coefficients show the effect of each channel. Radio had the biggest effect per unit of spend, at about 0.19 more sales per unit. TV had about 0.04 per unit, and Newspaper had almost no effect. Because TV budgets are much larger than Radio budgets, a company should compare the cost per unit of each channel before moving money from one to another.

## Limitations

- The dataset has 200 rows, which is small. A few unusual rows can change the results.
- The file does not include target segment or platform information, so the analysis covers advertising spend only.
- The units of spend and sales should be checked against the dataset's description before making business decisions.

## Next steps

- Check the units and add them to the results.
- Test whether the Newspaper channel can be removed without losing accuracy.
- Add segment or platform data, if available, to see which groups respond best to each channel.
