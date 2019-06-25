# Exercise 05 - Highlighting

1. Highlight the field name using fastVector highlighter 

```html
http://localhost:8983/solr/techproducts/select?hl=true&hl.method=fastVector&q=ipod&hl.fl=name&fl=id,name,cat&indent=on&q=*:*&wt=json
```

Response:

```JSON
{
  "responseHeader":{
    "status":0,
    "QTime":3,
    "params":{
      "q":["ipod",
        "*:*"],
      "hl":"true",
      "indent":"on",
      "fl":"id,name,cat",
      "hl.method":"fastVector",
      "hl.fl":"name",
      "wt":"json"}},
  "response":{"numFound":3,"start":0,"docs":[
      {
        "id":"IW-02",
        "name":"iPod & iPod Mini USB 2.0 Cable",
        "cat":["electronics",
          "connector"]},
      {
        "id":"F8V7067-APL-KIT",
        "name":"Belkin Mobile Power Cord for iPod w/ Dock",
        "cat":["electronics",
          "connector"]},
      {
        "id":"MA147LL/A",
        "name":"Apple 60 GB iPod with Video Playback Black",
        "cat":["electronics",
          "music"]}]
  },
  "highlighting":{
    "IW-02":{
      "name":["<em>iPod</em> & <em>iPod</em> Mini USB 2.0 Cable"]},
    "F8V7067-APL-KIT":{
      "name":["Belkin Mobile Power Cord for <em>iPod</em> w/ Dock"]},
    "MA147LL/A":{
      "name":["Apple 60 GB <em>iPod</em> with Video Playback Black"]}}}

``` 