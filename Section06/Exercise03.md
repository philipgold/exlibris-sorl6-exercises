# Exercise 03 - Pagination

1. Search for a query `q=*:*` and get the first five results sorted by `ID` in ascending order. 


```
http://localhost:8984/solr/techproducts/select?q=*:*&fl=id,name&start=0&rows=5&sort=id asc 
```

Response 
```json
{
  "responseHeader":{
    "status":0,
    "QTime":0,
    "params":{
      "q":["*:*",
        "*:*"],
      "indent":"on",
      "fl":"id,name",
      "start":"0",
      "sort":"id asc",
      "rows":"5",
      "wt":"json"}},
  "response":{"numFound":32,"start":0,"docs":[
      {
        "id":"0579B002",
        "name":"Canon PIXMA MP500 All-In-One Photo Printer"},
      {
        "id":"100-435805",
        "name":"ATI Radeon X1900 XTX 512 MB PCIE Video Card"},
      {
        "id":"3007WFP",
        "name":"Dell Widescreen UltraSharp 3007WFP"},
      {
        "id":"6H500F0",
        "name":"Maxtor DiamondMax 11 - hard drive - 500 GB - SATA-300"},
      {
        "id":"9885A004",
        "name":"Canon PowerShot SD500"}]
  }}
```

2. Fetch All Docs

The SolrJ pseudo-code shown here shows the basic logic involved in fetching all documents matching a query using a cursor:


```java
SolrQuery q = (new SolrQuery(some_query)).setRows(r).setSort(SortClause.asc("id"));
String cursorMark = CursorMarkParams.CURSOR_MARK_START;
boolean done = false;
while (! done) {
  q.set(CursorMarkParams.CURSOR_MARK_PARAM, cursorMark);
  QueryResponse rsp = solrServer.query(q);
  String nextCursorMark = rsp.getNextCursorMark();
  doCustomProcessingOfResults(rsp);
  if (cursorMark.equals(nextCursorMark)) {
    done = true;
  }
  cursorMark = nextCursorMark;
}
```

This by hand using curl, the sequence of requests would look something like this:
```bash
$ curl '...&rows=10&sort=id+asc&cursorMark=*'
{
  "response":{"numFound":32,"start":0,"docs":[
    // ... 10 docs here ...
  ]},
  "nextCursorMark":"AoEjR0JQ"}
$ curl '...&rows=10&sort=id+asc&cursorMark=AoEjR0JQ'
{
  "response":{"numFound":32,"start":0,"docs":[
    // ... 10 more docs here ...
  ]},
  "nextCursorMark":"AoEpVkRCREIxQTE2"}
$ curl '...&rows=10&sort=id+asc&cursorMark=AoEpVkRCREIxQTE2'
{
  "response":{"numFound":32,"start":0,"docs":[
    // ... 10 more docs here ...
  ]},
  "nextCursorMark":"AoEmbWF4dG9y"}
$ curl '...&rows=10&sort=id+asc&cursorMark=AoEmbWF4dG9y'
{
  "response":{"numFound":32,"start":0,"docs":[
    // ... 2 docs here because we've reached the end.
  ]},
  "nextCursorMark":"AoEpdmlld3Nvbmlj"}
$ curl '...&rows=10&sort=id+asc&cursorMark=AoEpdmlld3Nvbmlj'
{
  "response":{"numFound":32,"start":0,"docs":[
    // no more docs here, and note that the nextCursorMark
    // matches the cursorMark param we used
  ]},
  "nextCursorMark":"AoEpdmlld3Nvbmlj"}
```