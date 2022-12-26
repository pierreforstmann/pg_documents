# pg_documents

PostgreSQL extension providing JSON access to database with HTTP daemon 

Forked from https://github.com/markwkm/pg_documents

## Compiling

Compiling with PG 15.1 using PGXS works with **json-c-0.16-20220414** provided that json-c code is modified to avoid collision on `json_object` with:

```
find . -name '*.[ch]' -exec sed -i 's,json_object ,json_object_s ,g'  {} \;
find . -name '*.[ch]' -exec sed -i 's,json_object;,json_object_s; ,g'  {} \;
find . -name '*.[ch]' -exec sed -i 's,struct json_object$,struct json_object_s,g'  {} \;
find . -name '*.[ch]' -exec sed -i 's,struct json_object),struct json_object_s),g'  {} \;
```
