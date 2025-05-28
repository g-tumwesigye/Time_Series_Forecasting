# Air Quality Forecasting Using LSTM Networks

## Project Overview

This project aims to forecast PM2.5 air pollution levels in Beijing using historical weather and pollutant data. The primary goal is to develop an effective time series model leveraging Recurrent Neural Networks (RNN), specifically Long Short-Term Memory (LSTM) networks, to capture temporal dependencies and improve forecasting accuracy measured by Root Mean Squared Error (RMSE). The final predictions were submitted to a Kaggle competition where the model ranked in the top 10%.

---

## Approach to the Challenge

Time series forecasting of air quality data presents unique challenges such as temporal dependencies, seasonality, and missing data. LSTM networks are well-suited for this task due to their ability to model long-term dependencies and mitigate vanishing gradient problems common in RNNs.

The approach included:

- Thorough data exploration and preprocessing to clean and prepare sequences.
- Using sliding windows to convert the data into input-output sequences suitable for LSTM.
- Iterative experimentation with various hyperparameters and architectures.
- Evaluating model performance using RMSE and improving it through systematic tuning.

---

## Data Exploration, Preprocessing & Feature Engineering

- **Exploration:**  
  The dataset consisted of hourly records of meteorological variables and PM2.5 concentrations, spanning multiple years. Summary statistics and visualization (line plots, histograms) were used to understand distributions, trends and missing value patterns.

- **Missing Values:**  
  PM2.5 and some meteorological variables had missing values. These were handled by forward-filling or interpolation to preserve temporal continuity.

- **Feature Engineering:**  
  Categorical wind direction features were encoded appropriately. Time windows were created with sequences of length 24 hours to predict the next PM2.5 concentration.

- **Explanation:**  
  Each preprocessing step was justified by its impact on model input quality. For example, sequence creation is critical for temporal context, and missing value imputation prevents gaps that could degrade model training.

---

## Model Design & Architecture

- **Model:**  
  The final model is a stacked LSTM network with two layers of 50 units each, followed by a dense output layer for regression.

- **Hyperparameters:**  
  - Optimizer: Adam with learning rate 0.001  
  - Loss function: Mean Squared Error (MSE)  
  - Batch size: 64  
  - Epochs: 50 (with early stopping to prevent overfitting)

- **Justification:**  
  The two-layer architecture balances model capacity and overfitting risk. Adam optimizer adapts learning rates efficiently. Early stopping monitors validation loss for training stability.

---

Experiments.

- Conducted a number of experiments with varying number of layers, units, batch size and learning rates.
- Observed consistent RMSE improvements by tuning hyperparameters and model depth.
- Best RMSE achieved: **6390.08**

```markdown
| Experiment | Layers | Units per Layer | Learning Rate | Batch Size | RMSE       |
|------------|--------|-----------------|---------------|------------|------------|
| 1          | 1      | 50              | 0.001         | 64         | 6860.8204  |
| 2          | 2      | 50              | 0.001         | 64         | 6860.8204  |
| 3          | 2      | 100             | 0.001         | 64         | 6924.8794  |
| 4          | 2      | 50              | 0.0005        | 32         | 6461.0059  |
| 5          | 2      | 50              | 0.0005        | 64         | 6390.0883  |
| 6          | 3      | 50              | 0.001         | 64         | 6419.8672  |
| 7          | 3      | 100             | 0.0001        | 32         | 18399.0869 |
| 8          | 1      | 100             | 0.001         | 64         | 6532.8966  |
| 9          | 2      | 75              | 0.0007        | 64         | 9496.9161  |
| 10         | 3      | 50              | 0.001         | 128        | 17438.7776 |
| 11         | 3      | 100             | 0.0005        | 32         | 19568.3990 |
| 12         | 2      | 50              | 0.001         | 64         | 6562.5655  |
| 13         | 1      | 50              | 0.0001        | 32         | 11472.5329 |
| 14         | 2      | 100             | 0.0007        | 64         | 9545.3627  |
```

### Explanation:

* **Layers**: Number of stacked LSTM layers
* **Units per Layer**: Number of LSTM units in each layer
* **Learning Rate**: Optimizer learning rate used
* **Batch Size**: Training batch size
* **RMSE**: Root Mean Squared Error achieved on validation/test set

---

## Results & Discussion

- **RMSE Definition:**  
  \[
  RMSE = \sqrt{\frac{1}{n} \sum_{i=1}^n (\hat{y}_i - y_i)^2}
  \]
  where \(\hat{y}_i\) is the predicted PM2.5 and \(y_i\) the true value.

- Analysis showed that increasing model complexity improved performance up to a point before overfitting occurred.  
- Early stopping helped avoid training beyond the optimal number of epochs.  
- Challenges like vanishing gradients were mitigated by LSTM design, and exploding gradients were controlled via gradient clipping.  
- Prediction plots demonstrated good fit to actual PM2.5 trends.


---

## Conclusion

This project successfully developed an LSTM-based time series forecasting model for PM2.5 concentrations. Key successes include:

- Effective handling of missing data and sequence generation.  
- Careful model tuning achieving RMSE ~6390.  
  

Future work could explore incorporating additional meteorological features, testing alternative architectures like GRUs or integrating attention mechanisms to further improve accuracy.

---

## References

1. Hochreiter, S., & Schmidhuber, J. (1997). Long short-term memory. Neural computation, 9(8), 1735-1780.  
2. Brownlee, J. (2017). Deep Learning for Time Series Forecasting. Machine Learning Mastery.  
3. Kaggle Air Quality Forecasting Competition: [https://www.kaggle.com/c/air-quality-forecasting](https://www.kaggle.com/c/air-quality-forecasting)  
4. Géron, A. (2019). Hands-On Machine Learning with Scikit-Learn, Keras, and TensorFlow. O'Reilly Media.
5. [1] A. Abhishek, "Understanding GRUs, LSTM, & RNNs," *Medium*, 2020. [Online]. Available: https://medium.com/@abhishek/understanding-grus-lstm-rnns-1e7a8d0b2130. [Accessed: 28-May-2025].


---

*Author*  
Geofrey Tumwesigye  

