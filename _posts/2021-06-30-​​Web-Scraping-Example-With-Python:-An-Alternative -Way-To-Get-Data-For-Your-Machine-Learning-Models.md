---
layout: post
title: "Web Scraping Example With Python: An Alternative Way To Get Data For Your Machine Learning Models"
date:   2021-06-30 16:01:15 +0300

---
# Introduction 
It said that Is data is the new oil but like oil, it can be hard to get. If you are a data scientist like me you know enough or the right data plays an important role in having unbiased models. Even though there are many sources of free data you might not be interested in the ones available. Sometimes you just want something different or want to automate the process, instead of downloading every time the site is updated you just the process to happen in the background. in this post, we will be going through how to scrape data using beautiful soup and requests. for our example, we will be scraping Wikipedia tables and saving them to a CSV using pandas which is also a Python Library.

What Is A Web Scraping And Why Is It Important 
Web scraping is the process of automatically extracting data from websites. We write software programs to do this. We live in an information age where a lot of data is produced every minute, from social media, product reviews, news articles, e-commerce websites, stock prices/trends and so on. It is hard to keep up with the information. In most cases, we can’t just look at the data and find insights, you can’t keep switching between different applications for updates. Automating the process of information retrieval makes things easier, you can analyze your customer trends, find out when stock(even products on e-commerce like Amazon is available) drops or increases, get data from even websites that don’t allow copying and pasting actually you don’t have to even struggle copying and pasting. Such an exhausting process. The use cases of web scraping are a lot we can’t exhaust all of them.

## Assumption 
I assume you have basic knowledge about HTML and HTML tags. If you are not familiar with HTML tags check out [w3school](https://www.w3schools.com/html/default.asp) for a basic introduction.

# Data To Extract 
The first thing to do with web scraping is finding the website you want to get data from. In this post, we are going to extract [List of national independence](https://en.wikipedia.org/wiki/List_of_national_independence_days) days data from Wikipedia. now that we know the website we are getting data from below are the steps we are going to follow :

Steps 

1. Inspecting the website and finding the desired data/tags. 
This step is the most important step if you want to master web scraping. The inspection involves looking at the HTML, finding tags. 

2. Writing the code
We write the code that fetches the code, now that we know the HTML tags and elements we need we can get the data to manipulate it the way we want before storing it.

You can write this as a one-time use code or even automate it to run after a time interval.

3. Store the data in the desired format
After getting the data and manipulating it in ways we want we can save it in formats like CSV, JSON,txt, pdf and any media we want.

## Inspecting The Website And Finding The Data/Tags We Want To Extract
To inspect the website we need a way to see the HTML code behind what is being displayed. Thanks to modern browser extensions we can just do this by right-clicking and selecting inspect.

![List of nations](/img/posts/webscrape/list of nation .png)

After we clicking the inspect the developer tools window will be displayed and we can navigate to get our areas of interest.

Let us inspect some tags that we will be retrieving. When I click on the h1 tag in the developer window we see that the heading is highlighted. We know our heading is on h1 we will be using that to retrieve our heading.


![heading](/img/posts/webscrape/inspect header.png)

Let us look for the table tags and elements. when we select the table tag our table is selected. Now that we have found the tags to data we are interested in we can move on to implementing the code.

![heading](/img/posts/webscrape/inspect table .png)


## Implementation/Writing The Code 
We need to install the following python packages before using them.

* Requests – to get the data from the HTML webserver
* beautifulSoup -BeautifulSoup is one popular library provided by Python to scrape data from the web.
* pandas to save to csv
* Depending on your environment you might need to install lxml to parse the Html/XML.
Installing the pages 
```python 
#import packages 
import requests 
from bs4 import BeautifulSoup
import pandas as pd 
```
Beautifulsoup is managed under bs4 that’s why we import from there. you might be tempted to import directly

Send a GET request to the page server using the requests package 
```python 
#send request to website 
url = "https://en.wikipedia.org/wiki/List_of_national_independence_days"
html_content = requests.get(url).text
```
Parse our data and create a beautifulSoup object. Let us print some tags before we move on to using elements and beautiful soup functions.

```python
soup = BeautifulSoup(html_content, "lxml")
print(soup.title)

#That outputs
<title>List of national independence days - Wikipedia<title>

#To get the content inside the tags we add .text

soup = BeautifulSoup(html_content, "lxml")

print(soup.title.text)
```
This outputs a List of national independence days – Wikipedia which is the text under the tag.

We can print other tags such as paragraphs, headers etc some times tags such as paragraphs, headers can be many on one page and we need a way to collect a particular one based on its unique attributes. We might also want to collect all particular tags. beautifulSoup has two main methods we can use to do this:

find()- returns result when the searched element is found. Use this when you want to get one element.

find_all()- scans the whole document and returns all matches to the element.

Let us use table tag to find the table on the webpage.

```python 
tables = soup.find_all("table", class_="wikitable sortable")
print(len(tables))
``` 
Outputs 1 because only one table was found. When we print the table we get 

“wikitable sortable” as its class. You might have seen “wikitable sortable jquery-tablesorter ” but that appears after the table is sorted when the page loads. 

We are going to write code that loops through the table and puts values of given columns in a list. Let us look at these images to understand the structure before we implement the logic.

![heading](/img/posts/webscrape/inspect table row one.png)
![heading](/img/posts/webscrape/inspect table row two.png)

From the above images, we observe that when we click on tr(table row) a given row is selected. The table rows also have <td> tags nested in them and when you select one a given cell/column is selected.

Loop/Logic 

We are going to use find_all to find all rows(“tr” )of the table and within each row, we are going to use find_all  to find all cells(“td”) of the row. while looping through the rows we are going to check if the length of the cells list is equal to 6 and if so we shall extract their text and add it to a list according to their index in the cells list. 

```python 
country =[]
name_of_holiday =[]
date_of_holiday =[]
year_of_event =[]
independence_from =[]
event_notes =[]

#tbody
for row in tables[0].find_all('tr'):
    cells =row.find_all("td")
    if len(cells) ==6:
        country.append(cells[0].text.replace('\n', '').strip())
        name_of_holiday.append(cells[1].text.replace('\n', '').strip())
        date_of_holiday.append(cells[2].text.replace('\n', '').strip()) 
        year_of_event.append(cells[3].text.replace('\n', '').strip())
        independence_from.append(cells[4].text.replace('\n', '').strip())
        event_notes.append(cells[5].text.replace('\n', '').strip())                
```
We use a string method strip to remove the space that we got after replacing the newline escape sequence. This is one of the many manipulations you can do on the data before storing it. 

Store the data in the desired format

For we are going to store our data in a CSV using pandas. There are many formats you can save it in I just find CSV to be easy to use. With variable naming, space isn’t allowed that’s why our lists were in snakecase but we can name them the right way before saving to CSV.
```python 
df = pd.DataFrame({

'Country': country,
'Name of holiday': name_of_holiday,
'Date of holiday': date_of_holiday,
'Year of event':year_of_event,
'Independence from':independence_from,
"Event commemorated and notes":event_notes

})
df.to_csv('indepence_dates.csv', index=False)
```
At this point, you can even automate the process to run after a given period of time for example if you are scraping a news site you can let it automatically run after 24 hours, maybe every 10 minutes if it’s a stock site.

Below is part of our CSV, we can now use it for analysis and much more.
![heading](/img/posts/webscrape/final csv .png) 
## Caution
Most websites allow scraping data to a small extent if it is for personal use for some it is illegal to scrape their data. Always check out the “robots.txt” file before scraping. You can access it by appending /robots.txt to the Url of your interest for example if you want to scrape https://napro.dev the robots file is at https://napro.dev/robots.txt.

Websites are always changing their tag HTML attributes this might break your code and if that happens just inspect it and change accordingly.

# Conclusion
If there is anything you should remember from this post it’s the key steps to web scraping which are  Inspecting the website and finding the desired data/tags, Writing the code, and lastly storing the data in your desired format. I encourage you to find other sites to scrape for practice.

Please check out my [youtube channel](https://www.youtube.com/channel/UC1p_MdyNCb_fEXVZIJ5weFA) and subscribe I will be posting more videos there.



