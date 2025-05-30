# ⚡ Power Plants Data Processing Task - Summer 2025 Internship ☀️

This repository contains the solution for the programming assignment focused on processing and analyzing power plant volume data. The primary goal was to implement the `PowerPlants` Python class to handle data ingestion, storage, and aggregation from various CSV sources.

---
## 📝 Project Overview

The task involves managing data for different power plants (gas and wind). Key functionalities include:
* Loading data sequentially from specified CSV files (`gas_fr_plants.csv`, `gas_plants.csv`, `wind_plants.csv`).
* Processing the loaded data, which includes standardizing country names, handling missing values (assumed as 0 for volume), and adding metadata like update timestamps.
* Saving the processed data into a central CSV file (`database.csv`) which acts as a simple database.
* Retrieving the most recently updated data for every power plant symbol from the database.
* Aggregating data to calculate monthly average, minimum, and maximum production volumes for each plant.
* Aggregating data to determine total power production by country and technology type.

---
## 🛠️ Core Component: `PowerPlants` Class

The solution revolves around the `PowerPlants` class, which encapsulates all the required data handling logic.

### Key Methods:
* **`__init__(self)`**: Initializes the class, setting the path for the database file.
* **`load_new_data_from_file(self, file_path: str)`**:
    * Loads data from a given CSV file.
    * Standardizes column names.
    * Maps country codes/names to full names (e.g., 'FR' to 'France').
    * Fills missing volume data with 0.
    * Adds `updatedby` and `updatetime` metadata columns.
* **`save_new_data(self, input_data: pd.DataFrame)`**:
    * Appends the processed DataFrame to `database.csv`.
    * Creates `database.csv` with headers if it doesn't already exist.
* **`get_data_from_database(self)`**:
    * Reads `database.csv`.
    * Returns a DataFrame containing only the most recently updated entry for each unique plant-date combination, based on the `updatetime` column.
* **`aggregate_data_to_monthly(self)`**:
    * Calculates the monthly average, minimum, and maximum production volume for each power plant.
    * Returns a DataFrame with a monthly index and columns formatted as "PlantName Statistic" (e.g., "Blenod-5 Min").
* **`aggregate_data_to_country(self)`**:
    * Calculates the total power production volume, grouped by country and technology type.
    * Returns a DataFrame with `country`, `Technology`, and total `Volume`.

---
