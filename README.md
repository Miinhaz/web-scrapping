
## 🕸️ Web Scraping Project: Largest Companies in the U.S. by Revenue

This project demonstrates how to scrape data from Wikipedia to extract information about the largest companies in the United States by revenue. The script uses the `requests` library to fetch the webpage and `BeautifulSoup` for parsing the HTML content.

### 🛠️ Technologies Used
- **Python**
- **BeautifulSoup**: For parsing HTML and XML documents.
- **Requests**: For making HTTP requests to retrieve web content.
- **Pandas**: For data manipulation and saving the scraped data to a CSV file.

Below is a breakdown of the main components of the script:

### 1. Importing Libraries
```python
from bs4 import BeautifulSoup
import requests
```
We start by importing the necessary libraries:
- **BeautifulSoup** from `bs4` for parsing HTML and XML documents.
- **requests** to send HTTP requests and retrieve web pages.

### 2. Defining the URL and Sending a Request
```python
url = 'https://en.wikipedia.org/wiki/List_of_largest_companies_in_the_United_States_by_revenue'
page = requests.get(url)
```
We define the URL of the Wikipedia page and use `requests.get()` to fetch the content of the page.

### 3. Parsing the HTML
```python
soup = BeautifulSoup(page.text, 'html')
```
We create a BeautifulSoup object by passing the page content and specifying the parser. This allows us to navigate and search through the HTML structure easily.

### 4. Finding the Table
```python
table = soup.find_all('table')[0]
```
We locate the first table in the HTML, which contains the relevant data about the companies.

### 5. Extracting Column Titles
```python
world_titles = table.find_all('th')
world_table_titles = [title.text.strip() for title in world_titles]
```
We extract the headers of the table (column titles) by finding all `<th>` elements and stripping any whitespace to clean the text.

### 6. Creating a DataFrame
```python
import pandas as pd
df = pd.DataFrame(columns=world_table_titles)
```
Using the **Pandas** library, we create an empty DataFrame with the extracted column titles, which will store the scraped data.

### 7. Extracting Row Data
```python
column_data = table.find_all('tr')
for row in column_data[1:]:
    row_data = row.find_all('td')
    individual_row_data = [data.text.strip() for data in row_data]
```
We loop through each row of the table (skipping the header row) and extract the data from each cell (`<td>` elements). Each cell's text is cleaned and stored in a list.

### 8. Storing Data in the DataFrame
```python
length = len(df)
df.loc[length] = individual_row_data
```
We append the cleaned data from each row to the DataFrame.

### 9. Saving Data to CSV
```python
df.to_csv(r'J:\WEB SCRAPPING\companies.csv', index=False)
```
Finally, we save the DataFrame as a CSV file, allowing for easy access and analysis of the scraped data.

---

Feel free to modify any parts or add additional details as you see fit!
