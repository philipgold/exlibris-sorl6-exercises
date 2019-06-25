# Exercise 04 - eDisMax Query Parser 


All of the sample URLs in this section assume you are running Solr’s “techproducts” example:
```bash
bin/solr -e techproducts
```

1. Boost the result of the query term "hello" based on the document’s popularity:

```URL
http://localhost:8983/solr/techproducts/select?defType=edismax&q=hello&pf=text&qf=text&boost=popularity
```

2. Search for iPods OR video:

```URL
http://localhost:8983/solr/techproducts/select?defType=edismax&q=ipod+OR+video
```

3. Search across multiple fields, specifying (via boosts) how important each field is relative each other:

```URL
http://localhost:8983/solr/techproducts/select?q=video&defType=edismax&qf=features^20.0+text^0.3
```

4. Boost results that have a field that matches a specific value:

```URL
http://localhost:8983/solr/techproducts/select?q=video&defType=edismax&qf=features^20.0+text^0.3&bq=cat:electronics^5.0
```

5. Us the "mm" param, 1 and 2 word queries require that all of the optional clauses match, but for queries with three or more clauses one missing clause is allowed:

```html
http://localhost:8983/solr/techproducts/select?q=belkin+ipod&defType=edismax&mm=2
http://localhost:8983/solr/techproducts/select?q=belkin+ipod+gibberish&defType=edismax&mm=2
http://localhost:8983/solr/techproducts/select?q=belkin+ipod+apple&defType=edismax&mm=2
```

6. Override of the qf parameter being used to alias "name" in the query string to either the “last_name” and “first_name” fields:

```html
defType=edismax
q=sysadmin name:Mike
qf=title text last_name first_name
f.name.qf=last_name first_name
```
