---
layout: posts
title:  "Searching for elastic"
---

After reviewing the [video guide](https://www.elastic.co/webinars/getting-started-elasticsearch?baymax=default&elektra=docs&storm=top-video) on elastic's website, it seems like it could be easy to just grab the executable and start it (now that Java comes with the program). 

## Quick start

1. download the file (elastic search)
2. execute the file

Alternatively, it looks docker can do it too:

```
docker run -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" docker.elastic.co/elasticsearch/elasticsearch:7.10.1
```
Depending on your preference, it could be favorable to install the local package:

```
wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.10.2-amd64.deb.sha512
$ shasum -a 512 -c elasticsearch-7.10.2-amd64.deb.sha512
$ sudo dpkg -i elasticsearch-7.10.2-amd64.deb
$ sudo /bin/systemctl daemon-reload
$ sudo /bin/systemctl enable elasticsearch.service
$ sudo /bin/systemctl start elasticsearch.service
$ curl -X GET "localhost:9200/?pretty"
```
Perhaps it's best to just pick a path and get started.

----

 ## For Ubuntu 20.04
 
 [Install elastic](https://www.elastic.co/guide/en/elasticsearch/reference/current/deb.html) then [install kibana](https://www.elastic.co/guide/en/kibana/current/deb.html). Restart both services and visit [the elastic search page on localhost](http://localhost:5601).
 
 ### Collect Data
 
 [Auditd logs](https://www.elastic.co/guide/en/beats/filebeat/7.11/filebeat-module-auditd.html) could be a great place to start. Also, you might want to [install Metricbeat on the same server as Elasticsearch](https://www.elastic.co/guide/en/beats/metricbeat/7.11/metricbeat-installation-configuration.html) to monitor your server.
 

