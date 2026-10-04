# Kenya Maize Price Forecasting Using LSTM

## A Machine Learning Early-Warning System for Maize Price Spikes in Kenya

> Can an LSTM neural network learn historical maize price patterns well enough to forecast future prices and provide an early warning of potential maize price spikes in selected Kenyan markets?

**Author:** Emmilio Burure  
**Programme:** Zindua School — Data Science  
**Project Type:** Machine Learning Capstone



## Project Overview

Maize is one of Kenya's most important staple foods, making maize prices an important indicator of food affordability and household welfare.

However, maize prices can vary substantially between markets and over time. Sudden price increases can place additional pressure on households, farmers, traders, and organisations responsible for food-security planning.

This project uses historical maize price data from selected Kenyan markets to build a **Long Short-Term Memory (LSTM) neural network** for time-series forecasting.

The project goes beyond simply predicting future prices. The forecasts will also be used to develop a simple **price-spike early-warning system** that identifies periods where a significant increase in maize prices may occur.

The project therefore combines:

- Exploratory Data Analysis
- Time-series analysis
- Sequence modelling
- LSTM neural networks
- Hyperparameter tuning
- Time-aware model validation
- Forecast evaluation
- Price-spike detection

A simple **Naive forecasting model** will be used as a baseline to determine whether the LSTM provides meaningful improvement over a basic forecasting approach.

---

## Problem Statement

Maize prices in Kenya can experience substantial changes over time and can differ considerably between markets.

Price increases can affect:

- Low-income households through higher food costs
- Farmers through changing selling and storage decisions
- Traders and millers through changes in purchasing and inventory decisions
- Government agencies through food-security planning
- Humanitarian organisations through the planning of food and cash assistance

Forecasting these changes is challenging because maize prices may contain:

- Long-term trends
- Seasonal patterns
- Short-term fluctuations
- Sudden price spikes
- Market-specific behaviour

Traditional forecasting approaches may struggle to capture complex temporal relationships.

This project investigates whether an **LSTM neural network**, which is designed to learn patterns from sequential data, can effectively forecast maize prices in selected Kenyan markets.

---

## Research Questions

### Main Research Question

> **Can an LSTM neural network accurately forecast maize prices in selected Kenyan markets using historical price patterns?**

### Supporting Research Question

> **Can LSTM forecasts be used to identify potential significant maize price increases early enough to provide a useful warning?**

---

## Objectives

### General Objective

To develop an LSTM-based machine learning model for forecasting maize prices in selected Kenyan markets and use the forecasts to support an early-warning system for potential price spikes.

### Specific Objectives

1. Clean and prepare historical maize price data from selected Kenyan markets.

2. Explore trends, seasonality, market differences, volatility, and price spikes in the historical data.

3. Develop a simple Naive forecasting baseline.

4. Develop an LSTM neural network for maize price forecasting.

5. Tune the LSTM model's hyperparameters to improve forecasting performance.

6. Evaluate the model using time-aware validation and appropriate forecasting metrics.

7. Forecast maize prices one and three months ahead.

8. Develop a simple early-warning mechanism for identifying potential significant price increases.

9. Evaluate the effectiveness of the early-warning system using classification metrics.

---

# Data

## Data Source

The primary dataset is the:

**World Food Programme (WFP) Kenya Food Prices Dataset**, distributed through the **Humanitarian Data Exchange (HDX)**.

The dataset contains historical food prices recorded across markets in Kenya.

