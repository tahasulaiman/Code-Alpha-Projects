# Car Price Prediction with Machine Learning

This project predicts the selling price of used cars from their features. I trained two regression models and compared how well each one predicted prices on cars it had not seen before.

- **Linear Regression** is the simple baseline. It finds a straight-line relationship between the features and the price.
- **Random Forest** combines many decision trees. It can capture more complex patterns, but it can also make large mistakes on unusual cars.

## Dataset

The dataset is `car data.csv`, with 301 rows and 9 columns:

| Column | Meaning |
|---|---|
| Car_Name | Name of the car model |
| Year | Year the car was manufactured |
| Selling_Price | Price the car is being sold for (in lakhs). This is the value the models predict. |
| Present_Price | Current showroom price of the car (in lakhs) |
| Driven_kms | Kilometres the car has been driven |
| Fuel_Type | Petrol, Diesel or CNG |
| Selling_type | Dealer or Individual |
| Transmission | Manual or Automatic |
| Owner | Number of previous owners |

## Cleaning and feature engineering

1. **Removed 2 duplicate rows**, leaving 299 rows.
2. **Removed `Car_Name`**, because it has too many different values to encode usefully.
3. **Replaced `Year` with `car_age`** (2026 minus the year). Age is easier for a model to learn from than the year itself.
4. **Converted text columns to numbers** using one-hot encoding. This applies to `Fuel_Type`, `Selling_type` and `Transmission`.
5. **Split the data** into 80% for training and 20% for testing.

After these steps, the models use 8 features.

## Folder structure

```
car-price-prediction/
├── data/
│   └── car data.csv
├── images/
├── car_price_prediction.ipynb
└── README.md
```

## How to run

1. Keep `car data.csv` inside the `data` folder, next to the notebook.
2. Open `car_price_prediction.ipynb` in Jupyter Notebook, JupyterLab or Google Colab.
3. Run all cells from top to bottom. The results appear under the "Check the Results" section.

## Results

| Model | MAE (lakhs) | RMSE (lakhs) | R2 |
|---|---|---|---|
| Linear Regression | 1.47 | 2.52 | 0.75 |
| Random Forest | 1.47 | 3.51 | 0.52 |

**How to read the metrics:**
- **MAE** is the average size of a prediction error. Lower is better.
- **RMSE** is similar to MAE, but large errors count more. A higher RMSE than MAE suggests a few big mistakes.
- **R2** is how much of the price variation the model explains. Closer to 1 is better.

## What the results show

Linear Regression performed better on this data. Both models had almost the same MAE, but Random Forest had a much higher RMSE and a lower R2. The actual-vs-predicted plot shows why. Most cars were predicted well, especially the cheaper ones, but Random Forest predicted about 17 lakhs for a few cars that actually sold for 2 to 5 lakhs. It also under-predicted one very expensive car.

The feature importance chart shows that `present_price` matters most in the Random Forest model, with an importance of about 0.9. `Car_age` comes second at about 0.07. This makes sense, because a car's original showroom price is a strong guide to its used value.

## Limitations

- The dataset is small, with only 299 cars after cleaning. A few unusual cars can change the results a lot.
- The car age uses 2026 as the current year, so it would need updating if the data were used later.
- The models do not account for car condition, location or market demand, which also affect prices.

## Next steps

- Check the cars the models predicted badly to see if they have something in common.
- Add more data if it is available.
- Tune the Random Forest settings, such as the number of trees and the maximum depth of each tree.
- Use cross-validation to get a more reliable estimate of each model's performance.
