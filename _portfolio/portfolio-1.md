---
title: "Can AI Predict the Future of Solar Energy?"
excerpt: "A Transformer-based system for hour-ahead Global Horizontal Irradiance forecasting, with model comparison, hyperparameter optimization, and an interactive dashboard."
collection: portfolio
---

<div class="project-detail project-detail--solar" markdown="1">

<section class="project-detail__hero">
  <div>
    <p class="project-detail__eyebrow">Time-series research</p>
    <div class="project-detail__tags">
      <span>Transformers</span>
      <span>LSTM</span>
      <span>Solar energy</span>
      <span>Dash</span>
    </div>
    <h2>Forecasting sunlight one hour ahead.</h2>
    <p>A research project comparing Transformer and recurrent models for Global Horizontal Irradiance forecasting, supported by an interactive dashboard and a published preprint.</p>
    <div class="project-detail__actions">
      <a class="btn btn--info" href="https://github.com/Hamid701/GHI-Transformer-forecasting" target="_blank" rel="noopener">View on GitHub</a>
      <a class="btn" href="https://www.researchgate.net/publication/388350500_Transformer-Based_Global_Horizontal_Irradiance_Forecasting_A_Multi-Head_Attention_Approach_for_Hour-Ahead_Predictions" target="_blank" rel="noopener">Read the preprint</a>
    </div>
  </div>
  <img src="/images/transformer.jpg" alt="Illustration representing Transformer-based solar-energy forecasting">
</section>

## Overview 
As the world grapples with the challenges of global warming, renewable energy sources like solar power are becoming increasingly critical. However, integrating solar energy into electricity grids requires **accurate forecasting** of solar resources to balance supply and demand efficiently. Traditional forecasting models, such as ARIMA and LSTM, have shown promise but face limitations in handling long-term dependencies and computational efficiency.

In this project, I introduce a **novel Transformer-based approach** for **Global Horizontal Irradiance (GHI)** forecasting. By leveraging the **multi-head attention mechanism**, this model eliminates the sequential training bottleneck of recurrent models, enabling parallel processing and improving both accuracy and training speed. The results demonstrate a **20% reduction in Root Mean Squared Error (RMSE)** compared with the evaluated **LSTM model**.

### Why This Project Matters
Solar energy is inherently intermittent due to its dependence on weather conditions. Accurate GHI forecasts enable:

- **Optimized grid management** : Better integration of solar energy into existing grids.
- **Reduced operational costs** : Minimizing reliance on backup power sources.
- **Improved energy planning** : Enhancing decision-making for energy storage and distribution.

### Objective
This study implements advanced time-series forecasting models to predict **GHI** using hourly
historical data. The implementation includes state-of-the-art models such as **Transformer** and **LSTM**,
which focus on parallelization and handling long-term dependencies in time series data.

---

## Publication
You can read the preprint here:
- **Transformer-Based Global Horizontal Irradiance Forecasting: A Multi-Head Attention Approach for Hour-Ahead Predictions**  
  [Read the paper here](https://www.researchgate.net/publication/388350500_Transformer-Based_Global_Horizontal_Irradiance_Forecasting_A_Multi-Head_Attention_Approach_for_Hour-Ahead_Predictions)

---

## Key Features of the Project

### 1. Transformer-Based Architecture
The Transformer model uses a multi-head attention mechanism to capture both short-term and long-term dependencies in time series data. Unlike recurrent models, it processes all time steps simultaneously, enabling faster training and better generalization.

### 2. Interactive Dashboard
To make the model accessible and actionable, I developed an interactive dashboard using Dash and Plotly. Key features include:

- **Model comparison** : Compare predictions from Transformer and LSTM models.
- **Real-time metrics** : Visualize RMSE, nRMSE, MAE, and MASE for selected models.
- **Time range slider** : Focus on specific time periods for detailed analysis.
- **Download functionality** : Export prediction data as `.csv` files for further use.
  
### 3. Advanced Hyperparameter Optimization
Using state-of-the-art techniques like the Tree-Structured Parzen Estimator (TPE) algorithm, I optimized hyperparameters for both Transformer and LSTM models, ensuring optimal performance while minimizing computational overhead.

---

## Methodology

### Data Source
The dataset consists of **hourly GHI** from 2006 to 2015 for Rabat, Morocco (33.97°N, -6.85°E), provided by the **Copernicus Atmosphere Monitoring Service (CAMS)**. The data was preprocessed using a **sliding window approach** to generate labeled input-output pairs for supervised learning.

Below is a visualization of the hourly Global Horizontal Irradiance (GHI) data and its hourly distribution for Rabat, highlighting its variability over time.
<div align="center">
  <img src="/images/ghi_vs_time.png" alt="Time Series Visualization" width="45%">
  <img src="/images/GHI_Distribution_by_Hour.png" alt="GHI Distribution by Hour" width="45%"/>
  <img src="/images/Average_GHI_by_Month.png" alt="Average GHI by Month" width="45%">
  <img src="/images/GHI_Distribution_by_Season.png" alt="GHI Distribution by Season" width="45%"/>
</div>

1. **Daily Pattern**:
   - Clear diurnal cycle with peak values during mid-day.
   - Zero values during night hours.

2. **Seasonal Variation**:
   - Higher GHI values during the summer months.
   - Lower values during winter months.
   - Significant variation in day length across seasons.
     
### Model Design

The Transformer model uses a multi-head attention mechanism to capture both short-term and long-term dependencies in the data. Below is a simplified diagram of the architecture.

- **Input Embedding**: Maps the time series into a high-dimensional space.
- **Positional Encoding**: Encodes temporal order using sinusoidal functions.
- **Encoder Layers**: Four stacked encoder layers with multi-head self-attention and feed-forward networks.
- **Linear Layer**: Projects the final representation into a scalar value for GHI prediction.

<div align="center">
  <img src="/images/Transformer_str.png" alt=" Transformer architecture for forecasting one hour ahead of global horizontal irradiance (GHI)." width="700"/>
</div>

### Training Process
- **Transformer**: Achieved rapid convergence with minimal fluctuations in loss.
- **LSTM**: Showed slower convergence and higher error rates compared to the Transformer.

The training history of the Transformer and LSTM models is shown below. Notice how the Transformer converges faster and achieves lower validation errors.

<div align="center">
  <img src="/images/Transformer_training_history_20250211_124625.png" alt="Transformer Training History" width="45%"/>
  <img src="/images/LSTM_training_history_20250211_124625.png" alt="LSTM Training History" width="45%"/>
</div>

---

## Data Flow Diagram
The diagram below illustrates our ML pipeline architecture for processing GHI data:

<div align="center">
  <img src="/images/data_flow.png" alt="Data flow" width="70%"/>
</div>


--- 
## Results and Performance
The Transformer model outperformed all benchmark models across key metrics:

Evaluation Metrics:

| Model                 | RMSE  | nRMSE (%) | MAE   | MASE  |
|-----------------------|-------|-----------|-------|-------|
| **Transformer**       | 12.40 | 9.02      | 7.41  | 0.16  |
| **LSTM**              | 15.54 | 11.31     | 10.04 | 0.21  |
| **ARIMA**             | 18.09 | 13.45     | 16.12 | 0.35  |
| **Exp. Smoothing**    | 45.90 | 25.12     | 35.56 | 0.75  |
| **Persistence**       | 42.85 | 24.45     | 33.07 | 0.70  | 

<div align="center">
  <img src="/images/Model_Performance_Comparison.png" alt="Model Performance Comparison" width="70%"/>
</div>

These results highlight the Transformer's superior ability to capture complex temporal patterns, making it ideal for solar energy forecasting.

---

## Interactive Visualizations
The interactive dashboard provides an intuitive interface for exploring the model's predictions and performance metrics. Here’s a quick preview:

- **Model Comparison**: Compare predictions from Transformer and LSTM.
- **Time Range Slider**: Focus on specific time periods.
- **Metrics Display**: Real-time RMSE, nRMSE, MAE and MASE for selected models.
- **Download**: Download the predictions to your local device as .csv file.

### Full Video Demonstration
<div align="center">
  <video width="800" controls>
    <source src="/files/Dash-Preview.mp4" type="video/mp4">
    Your browser does not support the video tag.
  </video>
</div>

---

</div>

