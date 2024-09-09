# Final-Assignment.ipynb
Stock Data Analysis and Dashboard-Final Assignment.ipynb
To provide a complete and clear description and README for your Jupyter Notebook project, you can use the following template. This README will help others understand the purpose of your project, how to set it up, and how to run the provided code.

---

# Stock Data Analysis and Dashboard

## Description

This project involves extracting historical stock data and revenue data for Tesla and GameStop, and creating dashboards to compare stock prices with revenue. The project demonstrates the use of `yfinance` for financial data extraction and `BeautifulSoup` for web scraping. It includes the following tasks:

1. **Extract Tesla Stock Data Using yfinance:** Retrieve historical stock data for Tesla (TSLA) and process it into a DataFrame.
2. **Extract Tesla Revenue Data Using Webscraping:** Scrape revenue data for Tesla from a specified webpage and clean the data.
3. **Extract GameStop Stock Data Using yfinance:** Retrieve historical stock data for GameStop (GME) and process it into a DataFrame.
4. **Extract GameStop Revenue Data Using Webscraping:** Scrape revenue data for GameStop from a specified webpage and clean the data.

## Requirements

To run this project, you need the following Python packages:

- `yfinance` for financial data extraction
- `requests` for sending HTTP requests
- `beautifulsoup4` for HTML parsing
- `pandas` for data manipulation

You can install these packages using pip:

```bash
pip install yfinance requests beautifulsoup4 pandas
```

## Instructions

1. **Extract Tesla Stock Data**

   Use `yfinance` to extract Tesla stock data and display the first five rows of the DataFrame.

   ```python
   import yfinance as yf

   # Create Ticker object for Tesla
   tesla = yf.Ticker("TSLA")

   # Extract historical data
   tesla_data = tesla.history(period="max")

   # Reset the index
   tesla_data.reset_index(inplace=True)

   # Display the first five rows
   print(tesla_data.head())
   ```

2. **Extract Tesla Revenue Data**

   Use `requests` and `BeautifulSoup` to scrape Tesla revenue data from a specified webpage, clean the data, and display the last five rows of the DataFrame.

   ```python
   import requests
   from bs4 import BeautifulSoup
   import pandas as pd

   # URL for Tesla revenue data
   url = "https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/labs/project/revenue.htm"

   # Perform the HTTP request
   response = requests.get(url)
   html_data = response.text

   # Parse the HTML
   soup = BeautifulSoup(html_data, 'html.parser')

   # Find the table with revenue data (assuming it's the first table on the page)
   table = soup.find('table')

   # Read the table into a pandas DataFrame
   tesla_revenue = pd.read_html(str(table))[0]

   # Process the DataFrame
   tesla_revenue.columns = ['Date', 'Revenue']
   tesla_revenue['Revenue'] = tesla_revenue['Revenue'].str.replace(',|\$', "", regex=True)
   tesla_revenue.dropna(inplace=True)
   tesla_revenue = tesla_revenue[tesla_revenue['Revenue'] != ""]

   # Display the last five rows of the DataFrame
   print(tesla_revenue.tail())
   ```

3. **Extract GameStop Stock Data**

   Use `yfinance` to extract GameStop stock data and display the first five rows of the DataFrame.

   ```python
   import yfinance as yf

   # Create Ticker object for GameStop
   gamestop = yf.Ticker("GME")

   # Extract historical data
   gamestop_data = gamestop.history(period="max")

   # Reset the index
   gamestop_data.reset_index(inplace=True)

   # Display the first five rows
   print(gamestop_data.head())
   ```

4. **Extract GameStop Revenue Data**

   Use `requests` and `BeautifulSoup` to scrape GameStop revenue data from a specified webpage, clean the data, and display the last five rows of the DataFrame.

   ```python
   import requests
   from bs4 import BeautifulSoup
   import pandas as pd

   # URL for GameStop revenue data
   url = "https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/labs/project/stock.html"

   # Perform the HTTP request
   response = requests.get(url)
   html_data_2 = response.text

   # Parse the HTML
   soup = BeautifulSoup(html_data_2, 'html.parser')

   # Find the table with revenue data (assuming it's the first table on the page)
   table = soup.find('table')

   # Read the table into a pandas DataFrame
   gme_revenue = pd.read_html(str(table))[0]

   # Process the DataFrame
   gme_revenue.columns = ['Date', 'Revenue']
   gme_revenue['Revenue'] = gme_revenue['Revenue'].str.replace(',|\$', "", regex=True)
   gme_revenue.dropna(inplace=True)
   gme_revenue = gme_revenue[gme_revenue['Revenue'] != ""]

   # Display the last five rows of the DataFrame
   print(gme_revenue.tail())
   ```

## Screenshots

Make sure to include screenshots of the output for each step in your Jupyter Notebook. This includes:

- The output of the `tesla_data.head()`
- The last five rows of the cleaned `tesla_revenue` DataFrame
- The output of the `gamestop_data.head()`
- The last five rows of the cleaned `gme_revenue` DataFrame

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

This README template provides a clear overview of the project's goals, setup instructions, and how to run the code. Adjust the URLs and any specific details based on your actual project requirements.
