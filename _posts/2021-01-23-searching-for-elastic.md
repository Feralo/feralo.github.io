---
layout: posts
title:  "Searching for elastic"
---
https://www.elastic.co/webinars/getting-started-elasticsearch?baymax=default&elektra=docs&storm=top-video

Seems like it could be easy to just grab the executable and start it (now that Java comes with the program). 
Quick start

1. download the file (elastic search)
2. execute the file

Alternatively, it looks like I have been able to run it with docker in the past with this command:
`ocker run -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" docker.elastic.co/elasticsearch/elasticsearch:7.10.1`

```wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.10.2-amd64.deb.sha512
$ shasum -a 512 -c elasticsearch-7.10.2-amd64.deb.sha512
$ sudo dpkg -i elasticsearch-7.10.2-amd64.deb
$ sudo /bin/systemctl daemon-reload
$ sudo /bin/systemctl enable elasticsearch.service
$ sudo /bin/systemctl start elasticsearch.service
$ curl -X GET "localhost:9200/?pretty"```
