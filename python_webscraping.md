# Python Webscrapping
- [Back to Main](README.md)

[Webscraping](#webscraping)
1. [selenium](#selenium)
1. [threading](#threading)
1. [pyinstaller](#pyinstaller)
1. [example: google](#example-google)

# webscraping
Done best with
- Selenium - browser automation software
- WebDriver - explains Chrome to Selenium (ChromeDriver)
- Chrome - A web browser
- Webdriver-manager - managing different chromes on different computer
<p>
getting data online with apis: https://towardsdatascience.com/json-and-apis-with-python-fba329ef6ef0
</p>
See example webscraping for google in `google_search.py`

### selenium
- Selenium is browser automation software
- Use selenium version 4 (latest) or older to work properly with the WebDriver manager
```
pip install selenium
```

The version of Chrome on each persons computer is different, so we need to automatically change the WebDriver
using a WebDriver manager.

```
pip install webdriver-manager
```

``` python
from selenium import webdriver
from selenium.webdriver.chrome.service import Service as ChromeService
from webdriver_manager.chrome import ChromeDriverManager

driver = webdriver.Chrome(service=ChromeService(ChromeDriverManager().install()))
```

- using the WebDriver
``` python
from selenium.webdriver.chrome.options import Options
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
from selenium.webdriver.common.by import By
import time

chrome_options = Options()
chrome_options.add_argument("--headless") # might get bot detected if added
driver = webdriver.Chrome(service=ChromeService(ChromeDriverManager().install()), options=chrome_options)
driver.get("https://www.google.com/robots.txt")

dom_text = None
try:
    WebDriverWait(driver, 10).until(EC.presence_of_element_located(
        (By.TAG_NAME, "body")
    ))
    time.sleep(1.0) # if need extra time to wait for javascript
    
    main_element = driver.find_element(by=By.TAG_NAME, value="body")
    dom_text = main_element.text
finally:
    driver.close()
    driver.quit()
print(dom_text)
```

### threading
- Increase efficiency by running multiple tasks, others can run while others are waiting for the page to load
- Note the function in the thread cannot return anything, so must make changes through pointer parameters

``` python
from threading import Thread

# task function
def scrape_task(address, array):
    chrome_options = Options()
    chrome_options.add_argument("--headless")
    driver = webdriver.Chrome(service=ChromeService(ChromeDriverManager().install()), options=chrome_options)
    driver.get(address)

    dom_text = None
    try:
        WebDriverWait(driver, 10).until(EC.presence_of_element_located(
            (By.TAG_NAME, "body")
        ))
        time.sleep(1.0) # if need extra time to wait for javascript
        
        main_element = driver.find_element(by=By.TAG_NAME, value="body")
        dom_text = main_element.text
    finally:
        driver.close()
        driver.quit()
    
    array += [dom_text]

# run the tasks in threads
array = []
threads = [None] * 3
threads[0] = Thread(target=scrape_task, args=(f"https://google.com/robots.txt", array))
threads[1] = Thread(target=scrape_task, args=(f"https://google.com/robots.txt", array))
threads[2] = Thread(target=scrape_task, args=(f"https://google.com/robots.txt", array))
for i in range(len(threads)):
    threads[i].start() # start running the function
for i in range(len(threads)):
    threads[i].join() # don't continue until all the threads are complete

```

### pyinstaller
- For creating an executable file for Windows

```
pip install -U pyinstaller
```

Create the executable
```
pyinstaller ./main.py --onefile
```
If adding a specific chromedriver (but you should be using the manager above)
```
pyinstaller ./main.py --onefile --add-binary "./chromedriver_win32/chromedriver.exe;./chromedriver_win32"
```

### example: google

``` python
import requests
import urllib
from requests_html import HTMLSession

def get_source(url):
    """Return the source code for the provided URL. 
    Args: 
        url (string): URL of the page to scrape.
    Returns:
        response (object): HTTP response object from requests_html. 
    """

    try:
        session = HTMLSession()
        response = session.get(url)
        return response

    except requests.exceptions.RequestException as e:
        print(e)

def scrape_google(query):

    query = urllib.parse.quote_plus(query)
    response = get_source("https://www.google.co.uk/search?q=" + query)

    links = list(response.html.absolute_links)
    google_domains = ('https://www.google.', 
                      'https://google.', 
                      'https://webcache.googleusercontent.', 
                      'http://webcache.googleusercontent.', 
                      'https://policies.google.',
                      'https://support.google.',
                      'https://maps.google.')

    for url in links[:]:
        if url.startswith(google_domains):
            links.remove(url)

    return links

def get_results(query):
    
    query = urllib.parse.quote_plus(query)
    response = get_source("https://www.google.co.uk/search?q=" + query)
    
    return response

def parse_results(response):
    
    css_identifier_result = ".tF2Cxc"
    css_identifier_title = "h3"
    css_identifier_link = ".yuRUbf a"
    css_identifier_text = ".VwiC3b"
    
    results = response.html.find(css_identifier_result)

    output = []
    
    for result in results:

        item = {
            'title': result.find(css_identifier_title, first=True).text,
            'link': result.find(css_identifier_link, first=True).attrs['href'],
            'text': result.find(css_identifier_text, first=True).text
        }
        
        output.append(item)
        
    return output

def google_search(query):
    response = get_results(query)
    return parse_results(response)

print(google_search("floods"))
```