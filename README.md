# Python Web Scraper

Today's challenge is to build a web scraper using python.

## Requirements
* [Python 3](https://www.python.org/ftp/python/3.10.1/python-3.10.1-macos11.pkg) - Check if it is installed by typing `python3 --version` into your terminal
* [Google Chrome](https://www.google.com/chrome/)

## Installation

To get started, build and activate a new virtual environment.

```bash
mkdir python-virtual-environments && cd python-virtual-environments
python3 -m venv env
source env/bin/activate
```

## Usage

Install the `requests` and `selenium` libraries

```bash
python -m pip install requests
python -m pip install selenium
```

### requests

Let's create a new file called **scraper.py** and add the url of the website that you want to scrape. We are going to look at a test [Python Jobs webpage](https://realpython.github.io/fake-jobs/).

```python
import requests

URL = "https://realpython.github.io/fake-jobs/"
page = requests.get(URL)

print(page.text)
```

Now let's run the file and look at the output

```python
python scraper.py
```

Does it look like what you expect?

### selenium and chromedriver

We can also use selenium and chromedriver to scrape dynamic webpages. Selenium provides more options for parsing the webpage. To start, let's install `selenium` and `chromedriver` in your virtual environment:

```python
pip install selenium
pip install chromedriver
```

and add the following imports to our page:

```python
from selenium import webdriver
```

We will now use the webdriver to access the page instead of the `requests` module. Replace the requests function call and print command with the following:

```python
driver = webdriver.Chrome()

def launchBrowser():
  driver.get(URL)
  while(True):
    pass

launchBrowser()
```

This will, as the function name implies, launch the browser to the webpage we requested. Try it out!

We don't want to view the page, though, we want to pull data from it. Let's do a little bit of detective work on this page in the browser. Inspect the page using chrome developer tools. We want to target the company name on the first job posting.

![Dev Tools First Company Name](/assets/images/dev-tools-first-company-name.png)

Now let's use Selenium to parse the page and find that element. Add this to the `launchBrowser()` method below the `get` call.

```python
companies = driver.find_elements_by_class_name("company")
print(companies)
```

This provides a full list of the elements, which look like this:

```python
{'ELEMENT': '0.8520353655970223-1'}
```

Not very helpful. Let's debug!

## Resources
* [Beautiful Soup: Build a Web Scraper With Python](https://realpython.com/beautiful-soup-web-scraper-python/)
* [How to Use Selenium to Web-Scrape with Example](https://towardsdatascience.com/how-to-use-selenium-to-web-scrape-with-example-80f9b23a843a)
