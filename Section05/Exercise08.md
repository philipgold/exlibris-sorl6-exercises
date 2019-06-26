# Exercise 08 - Pagination

1. Search for a query `q=*:*` and get the first five results sorted by `ID` in ascending order. 


```
http://localhost:8983/solr/techproducts/select?q=*:*&fl=id,name&start=0&rows=5&sort=id asc 
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