# Muse EEG Headset Data Scrubber

## Overview

`DataScrub.py` processes EEG data collected using the Muse EEG headset, along with associated game behavior data. The script cleans and structures the data, making it suitable for further analysis using both Python and MATLAB. The output includes structured data in the form of dictionaries and data frames that can be saved and reused efficiently.

## Usage

1. **Set Up Environment:**
   Ensure you have the necessary Python libraries installed. Use the `requirements.txt` file for easy setup:
   ```bash
   pip install -r requirements.txt
   ```

2. **Run the Script:**
   Execute the script in a Jupyter notebook or an IPython environment to interact with the input widget.

3. **Provide CSV File:**
   Enter the file path to the Muse CSV file when prompted.

4. **View Processed Data:**
   The script will process the data and output structured dictionaries and data frames. Plots will be generated if `plot_data_aspects` is set to `True`.

5. **Save Data:**
   The processed data can be saved in both MATLAB and Python formats as specified in the script.


## How it works
1. [Input CSV](#Input-CSV)
2. [Modify Muse CSV](#Modify-Muse-CSV)
3. [Data Scrub: Muse File](#Data-Scrub-Muse-File)
    - [Bring into `pandas.DataFrame`](#Bring-into-pandas-DataFrame)
    - [Unique row components](#Unique-row-components)
    - [Helper Functions](#Helper-Functions)
    - [Data Structure Creation](#Data-Structure-Creation)
        - [Functional Data Structure](#Functional-Data-Structure)
            - [Dict: `eeg`](#Dict-eeg)
            - [Dict: `behavior`](#Dict-behavior)
        - [Description](#Description)
4. [Data Scrub: Game File](#Data-Scrub-Game-File)
    - [Modify/Input Space-separated File](#Modify-Input-Space-separated-File)
    - [Bring into `pandas.DataFrame`](#Bring-into-pandas-DataFrame)
    - [Dict: `game`](#Dict-game)
5. [Saving Data](#Saving-Data)
    - [Matlab Native](#Matlab-Native)
    - [Python Native](#Python-Native)
        - [Pickle Data Frames](#Pickle-Data-Frames)
        - [Pickle EEG / Behavior / Game Dictionaries](#Pickle-EEG-Behavior-Game-Dictionaries)

## Input CSV
- The script expects an input CSV file from the Muse EEG headset. The file path is provided via a widget interface.

## Modify Muse CSV
- The CSV file is modified to ensure it has the correct headers and removes unnecessary spaces to reduce file size.

## Data Scrub: Muse File
  - Bring into `pandas.DataFrame`
    - The modified CSV file is read into a pandas DataFrame for flexible data manipulation.
  - Unique row components
    - The unique components in the `Submod` column are identified and their counts are printed.
  - Helper Functions
    - Helper functions facilitate nested assignments in dictionaries and extract specific data rows.
  - Data Structure Creation
    - Functional Data Structure
      - Dict: `eeg`
        - The `eeg` dictionary contains the raw EEG data, relative and absolute power bands, and FFT data. Reference and DRL signals are handled separately.
      - Dict: `behavior`
        - The `behavior` dictionary includes signals related to headband connectivity, muscle movements, and head acceleration.
    - Description
      - Descriptive fields are added to the `eeg` and `behavior` dictionaries for context.

## Data Scrub: Game File
- The game file, which tracks game behavior, is processed similarly. It is read into a pandas DataFrame and converted into a dictionary.
  - Modify/Input Space-separated File
    - The game file is checked for headers and modified if necessary.
  - Bring into `pandas.DataFrame`
    - The game file is read into a pandas DataFrame for verification.
  - Dict: `game`
    - The game data is converted into a dictionary with numpy arrays for consistency and ease of saving.

## Saving Data
- Matlab Native
  - The structured data is saved in MATLAB format using `scipy.io.savemat`.
- Python Native
  - Pickle Data Frames
    - If specified, the pandas DataFrames for Muse and game data are saved using pickle.
  - Pickle EEG / Behavior / Game Dictionaries
    - The dictionaries for `eeg`, `behavior`, and `game` data are saved using pickle for efficient storage.

