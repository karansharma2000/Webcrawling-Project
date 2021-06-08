# Welcome to projects by Karan Sharma   ![width="10" height="10"](/images/7918BE1D-FD98-4360-86B1-5927F3DB2EA7.PNG)
All the projects done by Karan Sharma on github posted in one place
## Webcrawling
*Web scraping is extensively being used in many industrial applications today. Be it in the field of natural language understanding or data analytics, scraping data from websites is one of the main aspects of many such applications. Scraping of data from websites is extracting large amount of contextual texts from a set of websites for different uses. This project can also be extended for further use such as topic or theme based text summarization, news scraping from news websites, scraping of images for training a model etc.*

### Libraries Used:

To start with, let us discuss the several libraries that we are going to use in this project.

### requests:  

It is a library to send HTTP 1.1 requests very easily. Using requests.get method, we can extract a URL’s HTML content.
### urlparse: 

It provides a standard interface to break down a URL into different components such as network location, addressing scheme, path, etc.
### urljoin: 

It allows us to join a base URL with a relative URL to form an absolute URL.
### beautifulsoup:

It is a python library to extract data out of HTML and XML files. We can convert a HTML page to a beautifulsoup object and then extract HTML tags along with their contents


### Features:

The various aspects and features of the project.

1. Given an input URL and a depth upto which the crawler needs to crawl, we will extract all the URLs and categorize them into internal and external URLs.
2. Internal URLs are those which has the same domain name as that of the input URL. External URLs are those which has different domain name as that of the given input URL.
3. We check the validity of the extracted URLs. If the URL has a valid structure, only then it is considered.
4. A depth of 0 means that only the input URL is printed. A depth of 1 means that all the URLs inside the input URL is printed and so on.

```markdown
from urllib.request import urljoin
from bs4 import BeautifulSoup
import requests
from urllib.request import urlparse
  
  

links_intern = set()
input_url = "https://github.com/"
depth = 1
  

links_extern = set()
  
  

def level_crawler(input_url):
    temp_urls = set()
    current_url_domain = urlparse(input_url).netloc
  
    
    beautiful_soup_object = BeautifulSoup(
        requests.get(input_url).content, "lxml")
  

    for anchor in beautiful_soup_object.findAll("a"):
        href = anchor.attrs.get("href")
        if(href != "" or href != None):
            href = urljoin(input_url, href)
            href_parsed = urlparse(href)
            href = href_parsed.scheme
            href += "://"
            href += href_parsed.netloc
            href += href_parsed.path
            final_parsed_href = urlparse(href)
            is_valid = bool(final_parsed_href.scheme) and bool(
                final_parsed_href.netloc)
            if is_valid:
                if current_url_domain not in href and href not in links_extern:
                    print("External - {}".format(href))
                    links_extern.add(href)
                if current_url_domain in href and href not in links_intern:
                    print("Internal - {}".format(href))
                    links_intern.add(href)
                    temp_urls.add(href)
    return temp_urls
  
  
if(depth == 0):
    print("Internal - {}".format(input_url))
  
elif(depth == 1):
    level_crawler(input_url)
  
else:
  
    queue = []
    queue.append(input_url)
    for j in range(depth):
        for count in range(len(queue)):
            url = queue.pop(0)
            urls = level_crawler(url)
            for i in urls:
                queue.append(i)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/karansharma2000/projects/settings/pages). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out
