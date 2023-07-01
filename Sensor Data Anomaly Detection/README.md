# Sensor Data Anomaly Detection

## Background

In semiconductor industry, a wafer goes through fabrication process that involves various tools, and a recipe defines how the wafer is processed by a tool. A wafer lot is a batch of multiple wafers that belong to the same technology and product.

The sensor values of a tool are recorded for each wafer run, and this data is important for engineers to determine if the tool is working properly or not. Therefore, an FDC (fault detection and classification) system is necessary to detect any tool sensor anomalies to prevent further wafer scraps.

## Input Data

The input data is stored in a CSV file named "[Tool_Sensor_Data.csv](Tool_Sensor_Data.csv)".
The CSV file contains the wafer run information (e.g. TimeStamp, ToolName), and the columns with randomized characters denote the sensors. 

## Anomaly Detection Modelling and Pipeline Design

The task is to create a data science pipeline that performs anomaly detection of tool sensors. The solution should be able to predict whether a wafer run is anomalous or not. There are no labels (normal/anomalous) associated to the sensor data.

## Solution

Please find the "[solution.ipynb](solution.ipynb)" file for the solution.
