```markdown
<h1>Project Introduction</h1>

This project is a robust and configurable Python-based web scraping application designed to extract detailed product information from various e-commerce pages. It leverages a combination of `requests` for fetching web content and `BeautifulSoup` for parsing HTML, allowing it to systematically collect data points such as product name, description, price, rating, and review count. The scraper is built with features to enhance reliability and avoid detection, including dynamic proxy rotation, user-agent randomization, a robust retry mechanism for failed requests, and intelligent random delays between requests. All gathered data is efficiently organized and saved into a structured CSV file, ready for further analysis or integration.

<h2>Features</h2>

*   **Configurable Target URLs:** Easily specify a list of product URLs to scrape directly within the `config.py` file.
*   **Proxy Rotation:** Utilizes a pool of configured proxy servers to distribute requests, improving anonymity and reducing the risk of IP blocking.
*   **User-Agent Randomization:** Cycles through a list of common user-agent strings, mimicking different browsers to appear as a legitimate user.
*   **Robust Retry Mechanism:** Automatically retries HTTP requests that fail due to network issues or transient server errors, up to a defined maximum number of attempts.
*   **Intelligent Random Delays:** Introduces varying delays between requests to simulate human browsing patterns and prevent aggressive scraping behaviors that could lead to IP bans.
*   **Comprehensive Data Extraction:** Capable of parsing and extracting key product details:
    *   Product Name
    *   Product Description
    *   Price
    *   Customer Rating
    *   Number of Reviews
*   **CSV Output:** All extracted product data is cleanly compiled into a `data.csv` file, providing a tabular and easily accessible format.

<h2>Workflow Overview</h2>

The scraping process is designed for clarity and efficiency, following a structured sequence of operations:

1.  **Initialization:** The application begins by loading all necessary configuration settings, including the list of product URLs to target, available proxy servers, and a collection of user-agent strings from `config.py`. A user-agent rotator is set up for dynamic selection.
2.  **URL Iteration:** The scraper then proceeds to iterate through each product URL provided in the configuration.
3.  **Page Fetching:** For every URL, an HTTP GET request is made. This request is intelligently managed by:
    *   Selecting a random proxy from the configured list (if proxies are provided).
    *   Using a randomly chosen user agent from the available pool.
    *   Employing a built-in retry mechanism to handle temporary network issues or server unresponsiveness.
4.  **HTML Parsing & Data Extraction:** Upon successfully retrieving the web page's content, `BeautifulSoup` is used to parse the HTML. Specific selectors are applied to accurately locate and extract the desired product details (name, description, price, rating, reviews).
5.  **Data Aggregation:** The extracted details for each product are formatted as a dictionary and added to a master list that accumulates all scraped data.
6.  **Random Delay:** After processing each individual product page, a random delay (within a configurable range) is introduced before proceeding to the next URL. This helps prevent rapid-fire requests that might trigger bot detection.
7.  **Data Persistence:** Once all configured URLs have been processed, the accumulated product data is converted into a Pandas DataFrame and subsequently saved to the specified `data.csv` file.

<p>
    <img src="diagram_workflow.png" alt="Workflow Diagram" style="max-width: 100%;">
    <br>
    <em>This diagram illustrates the step-by-step workflow of the web scraper, from loading configurations to fetching, parsing, and ultimately saving the extracted product data to a CSV file. It highlights the iterative process for handling multiple URLs and the integration of proxy/user-agent rotation and delays.</em>
</p>

<h2>Example Output</h2>

The scraper generates a `data.csv` file that contains the structured product information. An example of the output format is shown below:

```csv
Product Name,Description,Price,Rating,Reviews
Product A,"Description for Product A.",$19.99,4.5,120
Product B,"Description for Product B. A bit longer to show detail.",$29.95,4.2,85
Product C,"Another product, excellent features!",$9.99,4.8,250
Product D,"Basic product description.",$10.50,3.9,45
Product E,"Premium quality item.",$49.00,4.7,300
```

<p>
    <img src="screenshot_success.png" alt="Screenshot of Successful Run" style="max-width: 100%;">
    <br>
    <em>This screenshot captures the console output of a successful scraping run, showing messages indicating the fetching and extraction progress for various product URLs, and confirming that the data has been successfully saved to `data.csv`.</em>
</p>

<p>
    <img src="screenshot_error.png" alt="Screenshot of Error Handling" style="max-width: 100%;">
    <br>
    <em>This screenshot illustrates an example of how the scraper handles and reports errors during execution, such as connection issues or maximum retries being reached for a specific URL, providing clear feedback on encountered problems.</em>
</p>

<h2>Getting Started</h2>

To set up and run this web scraping project on your local machine, please follow the instructions below:

<h3>Prerequisites</h3>

*   **Python 3.x**: Ensure you have Python 3.x installed. You can download it from the official Python website.

<h3>Installation</h3>

1.  **Obtain Project Files:** Make sure you have all project files (`main.py`, `config.py`, etc.) in a single directory on your local machine.

2.  **Install Required Libraries:** Open your terminal or command prompt, navigate to the project directory, and install the necessary Python packages using `pip`:
    ```bash
    pip install requests beautifulsoup4 pandas
    ```

<h3>Configuration</h3>

Before running the scraper, you **must** configure the `config.py` file according to your needs:

*   **`product_urls`**: Update this list with the full URLs of the product pages you wish to scrape.
*   **`proxies`**: Add a list of proxy server URLs (e.g., `http://host:port` or `http://user:pass@host:port`) if you want to use proxies. If left empty (`[]`), the scraper will not use proxies.
*   **`user_agents`**: You can customize or expand the default list of user-agent strings.
*   **`output_file`**: Change the name of the output CSV file if you prefer something other than `data.csv`.
*   **`max_retries`**: Adjust the maximum number of times the scraper will attempt to retry a failed HTTP request.
*   **`delay_range`**: Set the minimum and maximum seconds for the random delays between requests to control scraping speed.

<h3>Running the Scraper</h3>

1.  **Navigate to Project Directory:** Open your terminal or command prompt and change the directory to where your project files are located.
2.  **Execute the Script:** Run the main Python script:
    ```bash
    python main.py
    ```
3.  **View Output:** After the script completes its execution, a `data.csv` file will be generated in the same directory, containing all the extracted product information.

<h2>Tech Stack</h2>

*   **Python:** The primary programming language used for the entire application.
*   **Requests:** An elegant and simple HTTP library for Python, used for making web requests.
*   **BeautifulSoup4:** A Python library for pulling data out of HTML and XML files, used for parsing web page content.
*   **Pandas:** A powerful data analysis and manipulation library, used for structuring and saving the scraped data to CSV.
*   **Standard Python Libraries:** Includes `json` for data handling, `time` for implementing delays, and `random` for generating random values (e.g., for proxies, user-agents, and delays).

<h2>Author</h2>

The project author(s).
```