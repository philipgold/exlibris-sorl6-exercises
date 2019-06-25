# Exercise 02 - DisMax Query Parser
 

1. Get results for the word "video" using the `StandardRequestHandler` with the default search field:

>http://localhost:8983/solr/techproducts/select?q=video&fl=name+score

2. Activate "dismax" handler to search across the text, features, name, sku, id, manu, and cat fields all with varying boosts designed to ensure that "better" matches appear first, specifically: documents which match on the name and cat fields get higher scores.

>http://localhost:8983/solr/techproducts/select?defType=dismax&q=video

Note that this instance is also configured with a default field list, which can be overridden in the URL.

>http://localhost:8983/solr/techproducts/select?defType=dismax&q=video&fl=*,score


3. Override which fields are searched on and how much boost each field gets:

>http://localhost:8983/solr/techproducts/select?defType=dismax&q=video&qf=features^20.0+text^0.3

4. Boost results that have a field that matches a specific value.

>http://localhost:8983/solr/techproducts/select?defType=dismax&q=video&bq=cat:electronics^5.0

5. Register handler using the qt "instock" and has slightly different configuration options, notably: a filter for (you guessed it) inStock:true).

>http://localhost:8983/solr/techproducts/select?defType=dismax&q=video&fl=name,score,inStock

>http://localhost:8983/solr/techproducts/select?defType=dismax&q=video&qt=instock&fl=name,score,inStock


6. One of the other really cool features in this handler is robust support for specifying the "BooleanQuery.minimumNumberShouldMatch" you want to be used based on how many terms are in your user’s query. These allows flexibility for typos and partial matches. For the dismax handler, one and two word queries require that all of the optional clauses match, but for three to five word queries one missing word is allowed.

>http://localhost:8983/solr/techproducts/select?defType=dismax&q=belkin+ipod

>http://localhost:8983/solr/techproducts/select?defType=dismax&q=belkin+ipod+gibberish

>http://localhost:8983/solr/techproducts/select?defType=dismax&q=belkin+ipod+apple

7. Activate debugQuery option to viewing the parsed query, and the score explanations for each document.

>http://localhost:8983/solr/techproducts/select?defType=dismax&q=belkin+ipod+gibberish&debugQuery=true

>http://localhost:8983/solr/techproducts/select?defType=dismax&q=video+card&debugQuery=true