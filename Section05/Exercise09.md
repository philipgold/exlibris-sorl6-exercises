# Exercise 9 - Result Grouping 

1. Execute Grouping by field manu_exact", which specifies the manufacturers of items in the techproducts dataset.
 
 
```html
http://localhost:8983/solr/techproducts/select?fl=id,name&q=solr+memory&group=true&group.field=manu_exact&indent=on&q=*:*&wt=json
```

Response:
```json
{
  "responseHeader":{
    "status":0,
    "QTime":2,
    "params":{
      "q":["solr memory",
        "*:*"],
      "indent":"on",
      "fl":"id,name",
      "wt":"json",
      "group.field":"manu_exact",
      "group":"true"}},
  "grouped":{
    "manu_exact":{
      "matches":6,
      "groups":[{
          "groupValue":"Apache Software Foundation",
          "doclist":{"numFound":1,"start":0,"docs":[
              {
                "id":"SOLR1000",
                "name":"Solr, the Enterprise Search Server"}]
          }},
        {
          "groupValue":"Corsair Microsystems Inc.",
          "doclist":{"numFound":2,"start":0,"docs":[
              {
                "id":"VS1GB400C3",
                "name":"CORSAIR ValueSelect 1GB 184-Pin DDR SDRAM Unbuffered DDR 400 (PC 3200) System Memory - Retail"}]
          }},
        {
          "groupValue":"A-DATA Technology Inc.",
          "doclist":{"numFound":1,"start":0,"docs":[
              {
                "id":"VDBDB1A16",
                "name":"A-DATA V-Series 1GB 184-Pin DDR SDRAM Unbuffered DDR 400 (PC 3200) System Memory - OEM"}]
          }},
        {
          "groupValue":"Canon Inc.",
          "doclist":{"numFound":1,"start":0,"docs":[
              {
                "id":"0579B002",
                "name":"Canon PIXMA MP500 All-In-One Photo Printer"}]
          }},
        {
          "groupValue":"ASUS Computer Inc.",
          "doclist":{"numFound":1,"start":0,"docs":[
              {
                "id":"EN7800GTX/2DHTV/256M",
                "name":"ASUS Extreme N7800GTX/2DHTV (256 MB)"}]
          }}]}}}

```

2. Retrieve the top three results for the field memory for two price ranges of `0.00` to `99.99` and over `100`, using group.query.  

```html
http://localhost:8983/solr/techproducts/select?indent=true&fl=name,price&q=memory&group=true&group.query=price:[0+TO+99.99]&group.query=price:[100+TO+*]&group.limit=3

``` 

Response:
```json
{
  "responseHeader":{
    "status":0,
    "QTime":4,
    "params":{
      "q":["memory",
        "*:*"],
      "indent":["true",
        "on"],
      "fl":"name,price",
      "group.limit":"3",
      "group.query":["price:[0 TO 99.99]",
        "price:[100 TO *]"],
      "wt":"json",
      "group":"true"}},
  "grouped":{
    "price:[0 TO 99.99]":{
      "matches":5,
      "doclist":{"numFound":1,"start":0,"docs":[
          {
            "name":"CORSAIR ValueSelect 1GB 184-Pin DDR SDRAM Unbuffered DDR 400 (PC 3200) System Memory - Retail",
            "price":74.99}]
      }},
    "price:[100 TO *]":{
      "matches":5,
      "doclist":{"numFound":3,"start":0,"docs":[
          {
            "name":"CORSAIR  XMS 2GB (2 x 1GB) 184-Pin DDR SDRAM Unbuffered DDR 400 (PC 3200) Dual Channel Kit System Memory - Retail",
            "price":185.0},
          {
            "name":"Canon PIXMA MP500 All-In-One Photo Printer",
            "price":179.99},
          {
            "name":"ASUS Extreme N7800GTX/2DHTV (256 MB)",
            "price":479.95}]
      }}}}

```