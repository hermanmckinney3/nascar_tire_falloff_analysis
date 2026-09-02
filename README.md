# NASCAR Tire Falloff Analysis

This project uses race data from the `pynascar` API to calculate and visualize tire falloff for NASCAR Cup Series races from 2022–current (Next Gen era).

## Requirements

- `pynascar`
- `cup_tracks.csv` (provided in the repository files)

## Getting Started

### Installation

Start by installing `pynascar`:

```python
!pip install pynascar
```

For more information about the `pynascar` API wrapper and its available features, please visit the [PyNASCAR GitHub repository](https://github.com/ab5525/pynascar) by [@ab5525](https://github.com/ab5525).

This project also uses the provided `cup_tracks.csv` lookup file. The file contains track information, including track length, which is used to convert lap speed into lap time (seconds):

`lap_time = (track_length / lap_speed) * 3600`

### Imports

Import the required libraries and load the provided track lookup table:

```python
# Imports
import pandas as pd
import numpy as np
from pynascar import Schedule, Race, set_options
from pynascar import get_settings
from pynascar.driver import DriversData
import matplotlib.pyplot as plt

# CSV Import
track_lookup = pd.read_csv('cup_tracks.csv') # provided in the repository files
```

## Running the Analysis

The `analyze_track()` function requires two arguments: `track_name` and `driver_name`.

The function searches for available NASCAR Cup Series races at the selected track from 2022–current and produces tire falloff line charts for the selected driver. Each chart displays the driver's green-flag tire runs for an individual race.

Example:

```python
driver_data = analyze_track('New Hampshire Motor Speedway', 'Chase Briscoe')
driver_data
```

### Example Output

The function generates a tire falloff line chart for each available race
<img width="1339" height="770" alt="image" src="https://github.com/user-attachments/assets/11b08482-6d18-4ab0-af9d-38d8a2d9ac54" />

<img width="1335" height="761" alt="image" src="https://github.com/user-attachments/assets/00f1f645-d53e-47f5-a682-2723c57f0981" />

<img width="1336" height="766" alt="image" src="https://github.com/user-attachments/assets/119c8949-2e03-47ca-9a0f-a746725f18a9" />

<img width="1337" height="763" alt="image" src="https://github.com/user-attachments/assets/fff7bfd3-496c-40cb-a7ec-23fa06180ea4" />

### Reading the Visualization

- Each colored line represents a separate tire run.
- Tire age represents the number of green-flag laps completed on the current tire set.
- Lap times are filtered to remove abnormal laps that may result from cautions, pit cycles, weather, or other non-representative race conditions.

> **Note:** Version 1 does not distinguish between two-tire and four-tire pit stops when calculating tire age. This distinction will be addressed in Version 2 as the project expands.
