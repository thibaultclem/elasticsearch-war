# ElasticSearch encapsulate in eXo platform

This encapsulate an ElasticSearch in eXo Platform Server.
Only localhost request or username/password request can access.

## Configuring

1. Download `elasticsearch-http-basic-1.4.0.jar` on https://github.com/Asquera/elasticsearch-http-basic/releases
1. Create a new folder `es/plugins/http-basic` on the root of PLF server and copy/paste it the `elasticsearch-http-basic-1.4.0.jar`
1. Compile this module and copy/paste the `target/elasticsearch-war.war` to `webapp` folder of PLF Server
1. Start PLF


## Testing

After starting eXo Platform you can test as follow:

Authorized
```
$ curl -v localhost:9200 # works (returns 200) (localhost is configured as whitelisted ip)
$ curl -XPUT 'http://localhost:9200/blog/user/dilbert' -d '{ "name" : "Dilbert Brown" }'
$ curl -v --user root:gtn no_local_host:9200/blog # works (returns 200) (if credentials are set in configuration)
```

Not Authorized
```
$ curl -v --user root:notgtn no_local_host:9200/    # health check, returns 200 with  "{\"OK\":{}}" although Unauthorized
$ curl -v --user root:notgtn no_local_host:9200/    # health check, returns 200 with  "{\"OK\":{}}" although Unauthorized
$ curl -v --user root:notgtn no_local_host:9200/blog       # returns 401
```