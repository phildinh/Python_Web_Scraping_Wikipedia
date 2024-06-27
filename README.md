## Web Scraping from Wikipedia

### Lesson: 
Learned from Alex the Analyst (https://www.youtube.com/@AlexTheAnalyst). Shout out to his contributions!

### Target Wikipedia Page:
[List of largest companies in the United States by revenue](https://en.wikipedia.org/wiki/List_of_largest_companies_in_the_United_States_by_revenue)

### Resources:
- Python (Jupyter)
- pandas
- BeautifulSoup
- Requests

### Step 1: Introduction

```python
# Import the necessary libraries
from bs4 import BeautifulSoup
import requests
```

### Step 2: Fetch the Wikipedia Page
```python
# Define the URL of the Wikipedia page
url = 'https://en.wikipedia.org/wiki/List_of_largest_companies_in_the_United_States_by_revenue'

# Send a request to fetch the page
page = requests.get(url)

# Parse the HTML content of the page
soup = BeautifulSoup(page.text, 'html.parser')

# Print the parsed HTML content
print(soup)
```

### Step 3: Locate the Table
```python
# Find the first table in the HTML content
soup.find('table')
```

### Step 4: Identify the Desired Table
```python
# Find all tables in the HTML content and select the second table
soup.find_all('table')[1]

# Assign the desired table to a variable
table = soup.find_all('table')[1]

# Print the table to verify
print(table)
```

### Step 5: Extract Table Headers
```python
# Extract the headers of the table
word_titles = table.find_all('th')
word_titles
```

### Step 6: Get Table Headers
```python
# Get the text from each header and strip any extra whitespace
word_table_titles = [title.text.strip() for title in word_titles]
print(word_table_titles)
```

### Step 7: Create DataFrame and Add Headers
```python
# Import pandas library
import pandas as pd

# Create a DataFrame with the table headers
df = pd.DataFrame(columns=word_table_titles)
df
```

### Step 8: Locate Table Rows
```python
# Find all rows in the table
column_data = table.find_all('tr')
```

### Step 9: Extract Data and Populate DataFrame
```python
# Loop through each row in the table (excluding the header row)
for row in column_data[1:]:
    # Extract all data cells in the row
    row_data = row.find_all('td')
    
    # Get the text from each data cell and strip any extra whitespace
    individual_row_data = [data.text.strip() for data in row_data]
    
    # Get the current length of the DataFrame
    length = len(df)
    
    # Add the row data to the DataFrame
    df.loc[length] = individual_row_data
```

### Step 10: Save DataFrame to CSV
```python
# Display the DataFrame
df

# Save the DataFrame to a CSV file
df.to_csv(r' **COPY YOUR FILE PATH\YOUR NAME FILE.CSV', index=False)
```





