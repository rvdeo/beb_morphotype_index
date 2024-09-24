# Morphotype index calculator

This Python notebook analyzes beach profiles by determining concavity, segmentwise profile percentage, slope, and mean elevation from the given profile data.

This tool is designed to process beach profile data to:
1. Calculate and visualize the concavity of the profile.
2. Identify inflection points where the concavity changes.
3. Calculate the slope of the profile.
4. Segment the profile between inflection points and determine segmentwise concavity, percentage of the profile covered by each segment, and mean elevation.


## Requirements

Install all the required dependencies given in the requirements.txt file

## Function Overview

The key function in this notebook is `extract_profile`, which processes a given profile and date to generate the required analysis. Here's what the function does:

1. **Profile Extraction**:
   - Extracts a profile from the dataset based on `ProfileID` and `Date`.
   - Filters elevation values between 0 and 10 units for analysis. You can change the upper value (here 10) based on your datasets.
   
2. **Imaginary Line Calculation**:
   - Computes a linear interpolation between the first and last points of the profile to serve as a reference for concavity analysis.

3. **Inflection Point Detection**:
   - Identifies points where the profile crosses the imaginary line, which indicates changes in concavity.

4. **Concavity Analysis**:
   - Calculates concavity values along the profile and plots them. 
   
5. **Slope Calculation**:
   - Computes the overall slope of the profile in degrees. Slope was not included in the final PMI calculation, just to look at the profile gradient. 

6. **Segmentwise Analysis**:
   - Divides the profile into segments based on inflection points.
   - Computes the concavity, percentage, and mean elevation for each segment. Negative values indicate Concave segment, Positive values Convex, and zero indicate Linear 
     segement. Segment with the mean elevation less than or equal 0.1 m is considered as Linear. Ignore the segment which is less than 10% of the profile. 

## Data Structure

The input data is expected to be in a pandas DataFrame format, with the following columns:

- `ProfileID`: A unique identifier for each profile.
- `Date`: The date of the profile recording.
- `Distance`: The distance along the profile (x-coordinate).
- `Elevation`: The elevation value (y-coordinate).

## Usage

1. **Data Preparation**: Ensure that your input DataFrame has the correct structure with `ProfileID`, `Date`, `Distance`, and `Elevation` columns.
   
2. **Function Call**: Call the `extract_profile` function with the appropriate parameters:
   ```python
   extract_profile(dataframe, profile, date)
   ```

   - `dataframe`: The full DataFrame containing profile data.
   - `profile`: The specific `ProfileID` to analyze.
   - `date`: The date of the profile to analyze.

3. **Output**: The function will generate the following outputs:
   - A plot of the original profile and the imaginary line.
   - Inflection points marked on the plot.
   - Concavity plotted over the profile length.
   - Slope of the profile printed in degrees.
   - Segmentwise concavity, percentage, and mean elevation printed for each segment.

## Notes

- The profile data should be clean and well-structured. Any missing or incorrect values in the `Distance` or `Elevation` columns may lead to erroneous results.
- Ensure that the elevation values fall within the specified range (e.g., between 0 and 10 units) to get meaningful results.
- Inflection points are identified using changes in concavity, so profiles with few or no significant changes may result in minimal or no inflection points.
