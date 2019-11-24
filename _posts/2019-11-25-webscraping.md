---
layout: post
title: Webscraping and Python lessons 5 & 6
---

_Hello and welcome back to a very boring blog unless you're really into very old newspapers._
  
### Webscraping Process

The exercise required us to scrape the “Dispatch”, download all issues of “Richmond Times Dispatch” from 1860-1865, available [here](http://www.perseus.tufts.edu/hopper/collection?collection=Perseus:collection:RichTimes). This was done in the following steps.

1. Grab the source of the provided URL and paste into a regex editor. The URLs are in the format ```/text?doc=Perseus%3atext%3a2006.05.0001```. However this is just a link to the section of the site with embedded articles; the actual content is stored at URLs of the form ```http://www.perseus.tufts.edu/hopper/dltext?doc=Perseus%3Atext%3A2006.05.0001```.
2. Find just the URLS in regex using ```text\?doc=Perseus\%3atext\%3a2006\.05\.\d\d\d\d``` and remove the rest of the content. (After doing it this long way I realised I can also do the elegant short way ```text\?doc=Perseus[^"]+``` which finds all strings that start with ```text\?doc=Perseus``` and capture up until the first ```"```)
3. In order to switch the URLs from the browser view to the xml download, as well as switch from relative to absolute addressing in one go:  
**find** ```text\?```  
**replace** ```http://www.perseus.tufts.edu/hopper/dltext\?```
4. Save the output as a text file
5. Run wget in Termux (should already be installed as part of Termux setup)
6. Enter ```wget -i perseusissues.txt``` in the terminal to begin an enormous download.



### Python Codeacademy lessons

![](https://raw.githubusercontent.com/aliavahed/aliavahed.github.io/master/img/python2.png)
