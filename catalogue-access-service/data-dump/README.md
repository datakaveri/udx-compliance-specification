# Resource server data (Elasticsearch Dump)

Due to large size of datasets, its uploaded in drive ( and not in github/git LFS)

Please find the datasets at the link : https://drive.google.com/drive/folders/1mbllMFJJw146O5TJQILUXURj80eqh7Wp

The link contains the following sets:
1)Providers : cat_provider.json
2)Resource Servers : cat_resource_servers.json
3)Resource Groups : cat_resource_groups.json
4)Resource Items : cat_resource_items.json

# Create ES Index dump

Stack yaml (deploy in same swarm as es)-
```yaml
version: "3.4"

networks:
  overlay-net:
    external: true
    driver: overlay

services:

  logstash-test:
    image: docker.elastic.co/logstash/logstash:7.8.1
    deploy:
      replicas: 1
      placement:
        constraints:
          - "node.labels.database_node==true"
      restart_policy:
        condition: on-failure
        delay: 5s
        window: 10s
    networks:
      - overlay-net
    command: /bin/bash -c "while true; do sleep 30; done;"
```

Deploy stack -
```sh
docker stack deploy -c logstash-dump-stack.yml dump
```
Access container shell -
```sh
docker exec -it <container-id> /bin/bash
```
Install required plugins -
```sh
bin/logstash-plugin install logstash-input-elasticsearch logstash-output-csv
```
Create the logstah dump pipeline cfg -
```sh
vi pipeline/dump.cfg
```
```yaml
input {
         elasticsearch {
            hosts => "tasks.elasticsearch:9200"
        user => "user"
        password => "password"
            index => "index-to-dump"
          }
        }
        output {
          csv {
                fields => ["[id]","[fields from _source to retrieve in csv]"]
            path => "/tmp/csv-export.csv"
          }
        }
```
Run logstash with dump config -
```sh
bin/logstash -f pipeline/dump.cfg
```
Copy dump from container to host fs -
```sh
docker cp <container>:/tmp/csv-export.csv ./csv-export.csv
```

