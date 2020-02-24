---
layout: post
title: Removing Text Markup and Python lessons 7 & 8
---

_It is time to play with the Daily Dispatch again, and its old-timey articles_
  
    
### 1 Removing text markup

#### 1a Cleaning individual issues

``` import re, os

source = "./inputs/"
target = "./outputs/"

lof = os.listdir(source)
for f in lof:
  with open(source + f, 'r') as fin:
    copy = fin.read()       # grab the content of a file
    date = re.search(r'<date value=\"([\d-]+)\"',copy).group(1)       # extract a date for file naming
    newF = re.sub("<[^<]+>", "",copy)       # remove xml tags
  with open(target+date+".txt", 'w') as f9:       # name new file for each issue by its date
    f9.write(newF)
 ```
#### 1b Cleaning up each entry in an issue

``` import re, os

source = "./inputs/"
target = "./outputs/"

lof = os.listdir(source)
for f in lof:
  issueList = []
  with open(source + f, 'r') as fin:
    count = 0                 # counter to build into ID names
    copy = fin.read()
    date = re.search(r'<date value="([\d-]+)"',copy).group(1)  # extract date of an issue
    articles = re.split("<div3 ", copy)  # split issue into separate entries
    for article in articles[1:]:
      article = "<div3 " + article  # restore missing tag from beginning of entry
      entry = re.search(r'type="([^\"]+)"',article).group(1) # extract entry type
      article = re.sub("<[^<]+>", "", article) # strip tags
      article.strip() # strip white space
      entryID = date + "_" + entry + "_" + str(count) # build ID
      article = article + "\n"
      issueList.append(entryID + " " + article) # precede each entry with its ID
      count+=1
    anIssue = "\n".join(issueList) # merge all entries into one file
  with open(target+date+".txt", 'w') as f9:
    f9.write(anIssue)
 ```
  
### Python Codeacademy lessons
  
![](https://raw.githubusercontent.com/aliavahed/aliavahed.github.io/master/img/python3.png)
