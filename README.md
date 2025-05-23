# Wikipedia Scraping Using Python requests and BeautifulSoup

```python
from bs4 import BeautifulSoup
import requests
import pandas as pd
```

```python
url = "https://en.wikipedia.org/wiki/List_of_largest_companies_in_the_United_States_by_revenue"
page = requests.get(url)
soup = BeautifulSoup(page.text, 'html')
```

```python
table = soup.find_all('table')[0]
```

```python
titles = [title.text.strip() for title in table.find_all('th')]
```

```python
print(titles)
```

```python
df = pd.DataFrame(columns=titles)
```

```python
df
```

```python
column_data = table.find_all('tr')
```

```python
for row in column_data[1:]:
    row_data = row.find_all('td')
    individual_row_data = [data.text.strip() for data in row_data]
    # print(individual_row_data)
    index = len(df)
    df.loc[index] = individual_row_data
```

```python
df.to_csv("companies_scraped_data.csv", index = False)
```

```python
df
```
