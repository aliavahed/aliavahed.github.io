---
layout: post
title: Structuring Data and Python lessons 9 & 10
---

_In order to make Daily Dispatch more readable, let's turn all entries into a single TSV_
  
    
### 1 Converting to TSV



```
import re, os

source = "./inputs/"
target = "./outputs/"

lof = os.listdir(source)
theTSV = []
count = 0

for f in lof:
  with open(source + f, 'r') as fin:
    copy = fin.read()
    date = re.search(r'<date value="([\d-]+)"',copy).group(1)  # extract date
    articles = re.split("<div3 ", copy)   # split into entries
    for article in articles[1:]:
      article = "<div3 " + article # repair entry

      entry = re.search(r'type="([^\"]+)"',article).group(1)   # get entry type

      try:
        header = re.search(r'<head>(.*)</head>', article).group(1)  # look for a header (some are missing)
        header = re.sub("<[^<]+>", "", header)
      except:
        header = "No Header"

      article = re.sub("<[^<]+>", "", article)          # tidy up the body copy
      article = re.sub(" +\n|\n +", "\n", article)
      article = re.sub("\n+", " ", article)

      entryID = date + "_" + entry + "_" + str(count)  # build an ID for the entry

      article = article.replace("\t", " ")  # strip out any tabs
      
      aRecord = "\t".join([entryID,date,entry,header,article])  # make a record for a single entry
      count+=1
      theTSV.append(aRecord)  # add record to list
with open(target+"dispatchTSV.tsv", 'w') as f9:
  f9.write("/n".join(theTSV))  # join to single file with each entry on a new line
 ```
  
### Python Codeacademy lessons
  
![](https://raw.githubusercontent.com/aliavahed/aliavahed.github.io/master/img/python0910.png)
