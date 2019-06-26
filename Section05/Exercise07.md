# Exercise 07 - Suggester

We have configured the suggester and request handler for this suggester in solrconfig.xml. 

Now let's run the configured suggester and examine the response. 

Example: Let's search for elec and see how many suggestions are returned in response. 
 

```html
http://localhost:8983/solr/techproducts/suggest?suggest=true&suggest.build=true&suggest.dictionary=mySuggester&suggest.q=elec:
```

Response:

```json
{
  "responseHeader":{
    "status":0,
    "QTime":14},
  "command":"build",
  "suggest":{"mySuggester":{
      "elec:":{
        "numFound":3,
        "suggestions":[{
            "term":"electronics and computer1",
            "weight":2199,
            "payload":""},
          {
            "term":"electronics",
            "weight":649,
            "payload":""},
          {
            "term":"electronics and stuff2",
            "weight":279,
            "payload":""}]}}}}
```