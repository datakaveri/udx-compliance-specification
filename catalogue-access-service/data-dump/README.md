# Resource server data (Elasticsearch Dump)

Due to large size of datasets, its uploaded in drive ( and not in github/git LFS)

Please find the datasets at the link : https://drive.google.com/drive/folders/1mbllMFJJw146O5TJQILUXURj80eqh7Wp

The link contains the following sets:
1)Providers : cat_provider.json
2)Resource Servers : cat_resource_servers.json
3)Resource Groups : cat_resource_groups.json
4)Resource Items : cat_resource_items.json

# Create ES Index dump

##Installing elasticdump using docker

```
docker pull elasticdump/elastisearch-dump
```

##Running elasticsearch

- Create directory for data
  `mkdir data`
- Run elasticdump to download json data t0 `/data`

    - Provider data dump
      ```
      docker run --rm -ti -v /data:/tmp elasticdump/elasticsearch-dump \
      --input=http://<username>:<password>@production.es.com:9200/my_index \
      --output=/tmp/cat_provider.json \
      --type=data
      --searchBody="{\"query\":{\"bool\":{\"must\":[{\"match\":{\"type.keyword\":\"iudx:Provider\"}}]}},\"_source\":{\"excludes\":\"_word_vector\"}}"
      ```
    - Resource Server data dump
      ```
       docker run --rm -ti -v /data:/tmp elasticdump/elasticsearch-dump \
      --input=http://<username>:<password>@production.es.com:9200/my_index \
      --output=/tmp/cat_resource_servers.json \
      --type=data
      --searchBody="{\"query\":{\"bool\":{\"must\":[{\"match\":{\"type.keyword\":\"iudx:ResourceServer\"}}]}},\"_source\":{\"excludes\":\"_word_vector\"}}" 
      ```
    - Resource Group data dump
      ```
       docker run --rm -ti -v /data:/tmp elasticdump/elasticsearch-dump \
      --input=http://<username>:<password>@production.es.com:9200/my_index \
      --output=/tmp/cat_resource_groups.json \
      --type=data
      --searchBody="{\"query\":{\"bool\":{\"must\":[{\"match\":{\"type.keyword\":\"iudx:ResourceGroup\"}}]}},\"_source\":{\"excludes\":\"_word_vector\"}}" 
        ``` 
