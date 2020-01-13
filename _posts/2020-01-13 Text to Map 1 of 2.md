---
layout: post
title: Text to Map (1 of 2)
---

_Happy new year. I'm kind of sick of the Daily Dispatch_
  
    
### Scraping TGNs

The first step of this process involved scraping the issues of the Daily Dispatch for location information. This was done in the following steps:

1. Extract all ```<placeName>``` tags from the document into a list
2. Strip these down to just the tgn values contained
3. 



2. Find just the URLS in regex using   
```text\?doc=Perseus\%3atext\%3a2006\.05\.\d\d\d\d```   
and remove the rest of the content. (After doing it this long way I realised I can also do the elegant short way ```text\?doc=Perseus[^"]+``` which finds all strings that start with ```text\?doc=Perseus``` and capture up until the first ```"```)

**find** ```text\?```  

  

  
