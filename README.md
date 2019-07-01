


[![Build Status](https://travis-ci.org/mchirico/bh.svg?branch=master)](https://travis-ci.org/mchirico/bh)
[![codecov](https://codecov.io/gh/mchirico/bh/branch/master/graph/badge.svg)](https://codecov.io/gh/mchirico/bh)
# bh

## Steps 
```
mkdir ~/tmphistory
cd ~/tmphistory
cp  ~/Library/Application\ Support/Google/Chrome/Default/History ~/tmphistory/chrome.db
sqlite3 chrome.db


SQLite version 3.24.0 2018-06-04 14:10:15
Enter ".help" for usage hints.
sqlite> .tables
downloads                meta                     urls
downloads_slices         segment_usage            visit_source
downloads_url_chains     segments                 visits
keyword_search_terms     typed_url_sync_metadata
sqlite>

```

Now you can query history


```bash
SELECT 
  datetime(last_visit_time/1000000-11644473600, "unixepoch") as last_visited,
  datetime(last_visit_time/1000000-11644473600, "unixepoch",'localtime') as local_last_visited,   
  url, 
  title, 
  visit_count 
FROM urls;

```


### Safari

```bash
# You will need to give full access to term
cp ~/tmphistory
cp ~/Library/Safari/History.db Safari.db

sqlite3 Safari.db


```


```sql

SELECT 
  datetime(hv.visit_time + 978307200, 'unixepoch', 'localtime') as last_visited, 
  hi.url,
  hv.title
FROM 
  history_visits hv, 
  history_items hi 
WHERE 
  hv.history_item = hi.id;

```




### Mac History

```bash
log show --last 1m

```