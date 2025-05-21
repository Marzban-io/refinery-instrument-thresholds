# Refinery Instrument Thresholds Analyzer

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Marzban-io/refinery-instrument-thresholds/blob/main/your_notebook_name.ipynb)

This project provides a Python-based tool, runnable in Google Colab, for analyzing measurement data from refinery instruments (e.g., pressure and temperature transmitters) to suggest operational soft and hard limits. The primary goal of these limits is to help safeguard the **mechanical integrity** of the instruments, rather than defining process control limits. The measurements are also taken from two real devices for greater convenience

## Overview

In refinery operations, instruments are critical for monitoring and control. Over time, or due to specific events, these instruments can be subjected to conditions that might compromise their long-term reliability or lead to failure. This tool uses historical measurement data to:

1.  **Calculate statistical soft limits:** These are based on the typical operating range of the instrument, helping to identify unusual deviations that might warrant investigation.
2.  **Define hard limits:** These are typically based on the instrument's design specifications (e.g., design pressure/temperature), often with a safety factor, to prevent operation beyond its mechanical capabilities.
3.  **Visualize data and limits:** Provides clear plots showing the measurement trend against the calculated soft and hard limits, highlighting any excursions.
4.  **Generate a statistical summary:** Offers key statistics about the measurement data and the calculated limits.

This approach provides a data-driven methodology to complement engineering judgment in setting appropriate operational boundaries for critical instrumentation.

## Features

*   **Automated Limit Calculation:**
    *   **Soft Limits:** Calculated using Interquartile Range (IQR) multiples (e.g., `Q1 - 4.5*IQR` and `Q3 + 4.5*IQR`).
    *   **Hard Limits:** Calculated based on provided design values (e.g., `Design Value * 0.9` or `Design Value - Fixed Offset`).
*   **Data Visualization:** Generates plots showing:
    *   Measurement trend
    *   Soft Upper Limit
    *   Soft Lower Limit
    *   Hard Upper Limit
    *   Markers for data points exceeding soft limits
*   **Statistical Summary:** Outputs a comprehensive table with statistics including:
    *   Min, Max, Mean, Median, Standard Deviation, Variance, Range
    *   Quartiles (Q1, Q3) and IQR
    *   Calculated soft and hard limits
    *   Count of anomalies (excursions beyond soft/hard limits)
*   **Focus on Mechanical Integrity:** Limits are designed to protect the instrument itself, distinct from process control or alarm limits which serve different purposes.
*   **Easy to Use:** Designed to run in Google Colab with minimal setup.

## How It Works

The tool typically processes time-series data from an instrument.

1.  **Data Loading:** Reads measurement data (e.g., from a CSV file).
2.  **Statistical Analysis:** Calculates descriptive statistics. Quartiles (25th percentile - K1, 75th percentile - K3) and the Interquartile Range (IKA) are key for soft limits.
3.  **Soft Limit Calculation:**
    *   Soft Lower Limit: `K1 - (Multiplier * IKA)` (e.g., `K1 - 4.5 * IKA`)
    *   Soft Upper Limit: `K3 + (Multiplier * IKA)` (e.g., `K3 + 4.5 * IKA`)
4.  **Hard Limit Calculation:**
    *   These are based on user-provided (Design) values.
5.  **Visualization & Reporting:** Generates plots and summary tables as shown in the examples below.
