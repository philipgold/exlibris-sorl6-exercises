# Exercise 01 - Spellchecking
 
1. Search for cemera instead of camera. 

```HTML
http://localhost:8983/solr/techproducts/select?q=cemera
```

Response:

```JSON
{
  "responseHeader":{
    "status":0,
    "QTime":1,
    "params":{
      "q":["cemera",
        "*:*"],
      "indent":"on",
      "wt":"json"}},
  "response":{"numFound":0,"start":0,"docs":[]
  }}

```

2. Search for `delll ultra sharp` instead of `Dell UltraSharp`. 

```html
http://localhost:8984/solr/techproducts/spell?df=text&spellcheck.q=delll+ultra+sharp&spellcheck=true&spellcheck.collateParam.q.op=AND&indent=on&wt=json
```