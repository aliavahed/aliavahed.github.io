---
layout: post
title: Removing Text Markup and Python lessons 7 & 8
---

_It is time to play with the Daily Dispatch again, and its old-timey articles_
  
    
### 1 Removing text markup

#### 1a Cleaning individual issues

````import re, os

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
 ````

  
### Python Codeacademy lessons
  
![](https://raw.githubusercontent.com/aliavahed/aliavahed.github.io/master/img/python3.png)
