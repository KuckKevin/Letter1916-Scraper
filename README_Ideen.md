# Letters1916 Web Scraper

A Python script that automates searches on the [Letters 1916–1923](https://letters1916.ie/) digital archive using Selenium. It collects titles and links to letters matching a user-defined keyword and saves the results to a CSV file for further analysis.

---

## 🔍 Project Goal

This tool speeds up the process of searching for specific keywords in the **Letters 1916–1923** collection. Instead of manually entering search terms and copying links, the script automates:

- Searching the site
- Navigating through result pages
- Extracting letter titles and URLs
- Saving the results to a structured `.csv` file

---

## 📦 Requirements

- Python 3.8 or higher
- [Selenium](https://pypi.org/project/selenium/)
- [ChromeDriver](https://chromedriver.chromium.org/) (must match your installed version of Chrome)

Install Python dependencies with:

```bash
pip install selenium
```

---

## ⚙️ Setup

Make sure ChromeDriver is installed and available in your system path.

---

## 🚀 Usage

Open the script and define the keyword you'd like to search for:

```python
keyword = "Casement"
csv_name = f"letters1916_{keyword}_results.csv"
```

Then run the script:

```bash
python main.py
```

A CSV file like `letters1916_Casement_results.csv` will be created in the same directory.

---

## 🧪 Example Output

```csv
Letters on letter1916.ie for the keyword: Casement

Letter Name,Link
"Letter from Roger Casement",https://letters1916.ie/document/1234
"Casement's Final Letter",https://letters1916.ie/document/5678
...
```

---

## 🧱 How It Works

The script performs the following steps:

### 1. Open the Website
Using Selenium, a Chrome browser instance is launched and navigates to the [Letters 1916–1923](https://letters1916.ie/) homepage.

```python
driver = webdriver.Chrome()
driver.get("https://letters1916.ie/")
```

### 2. Search for Keyword
The script locates the search bar, enters the keyword, and submits the search.

```python
search_bar = driver.find_element(By.NAME, "search-bar")
search_bar.send_keys(keyword)
search_bar.send_keys(Keys.ENTER)
```

### 3. Extract Number of Results and Pages
It retrieves the number of results and how many pages of results exist. Special handling ensures robustness across single and multi-digit page numbers.

### 4. Extract Letter Titles and Links
On each page, the script collects all letter titles (`<h4><a>`) and their corresponding URLs, storing them in two synchronized lists.

```python
all_titles.append(titel.text)
all_links.append(link)
```

### 5. Handle Pagination
Pages are turned using a combination of two functions:
- `turn_page()`: For most pages
- `turn_page_three_to_four()`: Special case for page 3 due to a site-specific bug in the pagination layout

### 6. Save to CSV
All results are written to a CSV file. The structure:
- First line: description
- Blank line
- Header: `Letter Name`, `Link`
- Data rows for each letter

```python
writer.writerow(["Letter Name", "Link"])
```

### 7. Close Browser
After processing, the browser is cleanly closed:

```python
driver.quit()
```

---

## 📂 Project Structure

The code is modular, with functions for:
- `setup()` – browser setup
- `search_keyword()` – submit keyword search
- `get_letters()` – extract results
- `turn_page()` / `turn_page_three_to_four()` – navigate result pages
- `teardown()` – close browser

---

## 🧑‍💻 Author

Created by Yanic Dollhopf.

---

## 📄 License

This project is open-source. You can use, modify, and share it freely under the [MIT License](LICENSE).

---

## 🤝 Contributing

Contributions and improvements are welcome! Please open an issue or submit a pull request.
