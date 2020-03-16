---
layout: post
title: L13 Social Network Analysis
---

_More ways to play with the Dispatch_

In this assignment we needed to prepare places from the Dispatch for social network analysis. We had to created nodes for each of the places in the Daily Dispatch, and create edges between any places that co-occurred in an article. Then we had to import this into Gephi onto a map in order to observe the networks created. Try as I might, I *could not* get Gephi to work, it crashed over and over. I used the rollapp Gephi online tool, but it appears to be too unstable even for small problems - it could not even get through the Star Wars class work, let alone the larger and more complex Dispatch task. Below, the code I used to create the nodes and edges file. Note, the nodes file uses the output from L11, where I created a csv of all TGNS with their frequencies, lat and lon.
  
    
```
import re, os

source = "./inputs/"
target = "./outputs/"

lof = os.listdir(source)
count = 0
edgesDic = {}

def updateDic(dic, key):
    if key in dic:
        dic[key] += 1
    else:
        dic[key]  = 1

# creating edges from a list
import itertools
def edges(edgesList, edgesDic): #create edges for tgns from one article
    edges = list(itertools.combinations(edgesList, 2))
    for e in edges:
        key = "\t".join(sorted(list(e))) # A > B (sorted alphabetically, to avoid cases of B > A)
        updateDic(edgesDic, key) #increment edge count per article

for f in lof:
  with open(source + f, 'r') as fin: #extract tgns
    copy = fin.read()
    date = re.search(r'<date value="([\d-]+)"',copy).group(1)
    articles = re.split("<div3 ", copy)
    for article in articles[1:]:
      topList = []
      for t in re.findall(r"<placeName[^<]+</placeName>", article):
        m = re.search(r'\d{7}',t)
        if m:
          topList.append(m.group())
      edges(topList, edgesDic)
     # print(edgesDic)

edgeFileList = []
for key, value in edgesDic.items():
  edgeFileList.append("\t".join([key,str(value)]))
    
with open(target+"edges.tsv", 'w') as f9:
  f9.write("/n".join(edgeFileList))

nodeFileList =[]
with open(source + "/nodes/places.csv", 'r') as nodeSource:
  # places.csv counts freq of all tgns in the dispatch
  # each line reads `9-digit-freq TAB tgn TAB PlaceName TAB latval TAB lonval`
  tgnList = nodeSource.readlines() #split file into list of rows
  for each in tgnList:
    nodeFileList.append(re.search(r'^[^\t]+\t(.+)'),each) # remove first column (frequency) from each row
with open(target + "nodes.tsv", 'w') as f8:
  f8.write('/n'.join(nodeFileList)) # join new list together
  ```
