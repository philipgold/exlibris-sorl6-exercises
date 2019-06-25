# Exercise 09 - Pagination

1. Search for a query `q=*:*` and get the first five results sorted by `ID` in ascending order. 

http://localhost:8983/solr/techproducts/select?q=*:*&fl=id,name&start=0&rows=5&sort=id asc: 


{ "responseHeader":{ "status":0, "QTime":0, "params":{