# Exercise 05 - Faceting

1. Run range faceting.

Search query for iPod with faceting enabled and range for the field price from 1000 to 100000 

```bash
http://localhost:8983/solr/techproducts/select?defType=edismax&q=ipod&fl=id,name,price&facet=true&facet.range=price&facet.range.start=10&facet.range.end=20&facet.range.gap=5&indent=on&q=*:*&wt=json
``` 

Response: 

```JSON
{
  "responseHeader":{
    "status":0,
    "QTime":0,
    "params":{
      "facet.range":"price",
      "q":["ipod",
        "*:*"],
      "defType":"edismax",
      "facet.range.gap":"5",
      "indent":"on",
      "fl":"id,name,price",
      "facet":"true",
      "wt":"json",
      "facet.range.start":"10",
      "facet.range.end":"20"}},
  "response":{"numFound":3,"start":0,"docs":[
      {
        "id":"IW-02",
        "name":"iPod & iPod Mini USB 2.0 Cable",
        "price":11.5},
      {
        "id":"F8V7067-APL-KIT",
        "name":"Belkin Mobile Power Cord for iPod w/ Dock",
        "price":19.95},
      {
        "id":"MA147LL/A",
        "name":"Apple 60 GB iPod with Video Playback Black",
        "price":399.0}]
  },
  "facet_counts":{
    "facet_queries":{},
    "facet_fields":{},
    "facet_ranges":{
      "price":{
        "counts":[
          "10.0",1,
          "15.0",1],
        "gap":5.0,
        "start":10.0,
        "end":20.0}},
    "facet_intervals":{},
    "facet_heatmaps":{}}}

```

2. Run Pivot faceting. 
 
 In our techproducts, we need the stock availability based on the popularity of a category 
 

 ```URL
 http://localhost:8983/solr/techproducts/select?q=*:*&facet.pivot=cat,popularity,inStock&facet.pivot=popularity,cat&facet=true&facet.field=cat&facet.limit=5&rows=0&facet.pivot.mincount=2&indent=on&q=*:*&wt=json 
 ```
 
Response: 

```URL
{
  "responseHeader":{
    "status":0,
    "QTime":3,
    "params":{
      "q":["*:*",
        "*:*"],
      "facet.limit":"5",
      "facet.field":"cat",
      "facet.pivot":["cat,popularity,inStock",
        "popularity,cat"],
      "indent":"on",
      "rows":"0",
      "facet":"true",
      "wt":"json",
      "facet.pivot.mincount":"2"}},
  "response":{"numFound":32,"start":0,"docs":[]
  },
  "facet_counts":{
    "facet_queries":{},
    "facet_fields":{
      "cat":[
        "electronics",12,
        "currency",4,
        "memory",3,
        "connector",2,
        "graphics card",2]},
    "facet_ranges":{},
    "facet_intervals":{},
    "facet_heatmaps":{},
    "facet_pivot":{
      "cat,popularity,inStock":[{
          "field":"cat",
          "value":"electronics",
          "count":12,
          "pivot":[{
              "field":"popularity",
              "value":7,
              "count":4,
              "pivot":[{
                  "field":"inStock",
                  "value":false,
                  "count":2},
                {
                  "field":"inStock",
                  "value":true,
                  "count":2}]},
            {
              "field":"popularity",
              "value":6,
              "count":3,
              "pivot":[{
                  "field":"inStock",
                  "value":true,
                  "count":3}]},
            {
              "field":"popularity",
              "value":1,
              "count":2,
              "pivot":[{
                  "field":"inStock",
                  "value":false,
                  "count":2}]}]},
        {
          "field":"cat",
          "value":"currency",
          "count":4},
        {
          "field":"cat",
          "value":"memory",
          "count":3},
        {
          "field":"cat",
          "value":"connector",
          "count":2,
          "pivot":[{
              "field":"popularity",
              "value":1,
              "count":2,
              "pivot":[{
                  "field":"inStock",
                  "value":false,
                  "count":2}]}]},
        {
          "field":"cat",
          "value":"graphics card",
          "count":2,
          "pivot":[{
              "field":"popularity",
              "value":7,
              "count":2,
              "pivot":[{
                  "field":"inStock",
                  "value":false,
                  "count":2}]}]}],
      "popularity,cat":[{
          "field":"popularity",
          "value":6,
          "count":5,
          "pivot":[{
              "field":"cat",
              "value":"electronics",
              "count":3},
            {
              "field":"cat",
              "value":"hard drive",
              "count":2}]},
        {
          "field":"popularity",
          "value":7,
          "count":4,
          "pivot":[{
              "field":"cat",
              "value":"electronics",
              "count":4},
            {
              "field":"cat",
              "value":"graphics card",
              "count":2}]},
        {
          "field":"popularity",
          "value":1,
          "count":2,
          "pivot":[{
              "field":"cat",
              "value":"connector",
              "count":2},
            {
              "field":"cat",
              "value":"electronics",
              "count":2}]},
        {
          "field":"popularity",
          "value":10,
          "count":2}]}}}

```

3. Run Interval faceting

Faceting query for field `price >=10` and `price < 20` 

```URL
http://localhost:8983/solr/techproducts/select?q=*:*&facet=true&facet.interval=price&f.price.facet.interval.set=[10,20)
```