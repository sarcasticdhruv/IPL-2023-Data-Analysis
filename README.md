## Project - IPL DATA Analysis 2023

### Overview

The "IPL DATA Analysis 2023" project involves a detailed analysis of the dataset of the Indian Premier League (IPL) 2023, along with some historical data. The data is extracted using web scraping techniques with Selenium and BeautifulSoup from the official IPL statistics page (https://www.iplt20.com/stats/).

### Web Scraping Code

The project utilizes Python with Selenium for web scraping. The code automates the Firefox browser, navigates to the IPL statistics page, waits for the table to load, and extracts data using XPath. The extracted data is then stored in a CSV file named "leadersdata.csv."

```python
# Import necessary libraries
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from selenium import webdriver
from selenium.webdriver.firefox.service import Service
from webdriver_manager.firefox import GeckoDriverManager
from selenium.webdriver.common.by import By
import time
import csv

# Configure the service and obtain the GeckoDriver executable
gecko_driver_service = Service(GeckoDriverManager().install())

# Initialize the Firefox driver
driver = webdriver.Firefox(service=gecko_driver_service)

# Navigate to the IPL statistics page
driver.get("https://www.iplt20.com/stats/")

# Wait for the table to load
time.sleep(2)

# Find the table element using XPath
table = driver.find_element_by_xpath("/html/body/div[2]/div[4]/section/div/div[3]/div[4]/div[3]/div/div[1]/table")

# Get all the rows in the table
rows = table.find_elements_by_tag_name("tr")

# Create a CSV file to save the data
with open("leadersdata.csv", "w", newline="") as csvfile:
    writer = csv.writer(csvfile)

    # Fetch data from each row and write to CSV
    for row in rows:
        # Get all the cells in the row
        cells = row.find_elements_by_tag_name("td")

        # Fetch data from each cell and write to CSV
        row_data = [cell.text for cell in cells]
        writer.writerow(row_data)

# Close the browser
driver.quit()
```

### Data Analysis

#### Observation based on `data.info()`

- The dataset contains 21 entries and 12 columns.
- "Player," "Avg," and "SR" columns have non-null values for all entries.
- The memory usage of the DataFrame is approximately 2.1 KB.

#### Observation based on `data.describe()`

- Players have played an average of 10.95 matches.
- The average runs scored is around 286.19, with a minimum of 2 runs and a maximum of 890 runs.
- The average batting average is approximately 29.64, and the average strike rate is around 143.07.

#### Observation based on `data.head()` and `data.tail()`

- Shubhman Gill and RD Gaikwad performed exceptionally well.
- Some players, like BA Stokes and MM Ali, had lower scores.

### Data Visualization

The project includes various visualizations using Matplotlib:

1. Bar plot of Runs (R) by Player.
2. Histogram of Batting Average (Avg).
3. Scatter plot of Strike Rate (SR) vs. Runs (R).
4. Box plot of Batting Average (Avg).
5. Line plot of Runs (R) by Player.
6. Bar plot of Number of 50s and 100s by Player.
7. Pie chart of Number of Outs (Outs).
8. Bar plot of Number of 4s and 6s by Player.
9. Stacked bar plot of 50s and 100s by Player.
10. Area plot of Runs (R) by Player.

### Each Ball Data Analysis

- Scatter plot, Histogram, Box plot, and Line plot were created to analyze the relationship between match number and score.

### Each Match Data Analysis

#### Team Performance

1. Bar graph showing the number of matches won by each team.
2. Line graph depicting cumulative wins over time.

#### Toss Analysis

1. Pie chart displaying the percentage of toss wins by each team.
2. Stacked bar graph showing the toss decision by each team.

#### Player Performance

- Bar graph showcasing the top players with the most "Man of the Match" awards.

#### Venue Analysis

- Bar graph revealing the top venues with the most matches.

#### Match Outcome

- Pie chart illustrating the percentage of matches won by each team.

### Observations based on Visualizations

- Gujrat Titans performed exceptionally well, winning the maximum number of matches.
- Shubhman Gill and RD Gaikwad exhibited outstanding batting performances.
- Most teams preferred fielding after winning the toss.
- The Narendra Modi Stadium appeared to be more favorable for matches.
- Shubhman Gill and Yashasvi Jaiswal received the most "Man of the Match" awards.
- Gujrat Titans won the highest percentage of matches.

The visualizations provide valuable insights into player performances, team dynamics, and match outcomes throughout the IPL 2023 season.
