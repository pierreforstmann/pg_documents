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
Build the extension:
```
make
```
## Installing

```
make install`
cp /usr/local/lib64/libjson-c.so.5 $PGDATA/../lib
```

Add to postgresql.conf:
```
shared_preload_libraries='pg_documents'
pg_documents.database = 'pierre'
pg_documents.port='8000'
```
Restart PG instance:
```
pg_ctl stop
pg_ctl start
```
