---
layout: single
title: Elasticsearch cheatsheet
author: aNNufriy
tags: [elasticsearch]
cover_url: "/images/jekyll.png"
---

## Elasticsearch cheatsheet

Create index
```bash
PUT /tags
```
----
Create pipeline
``` bash
PUT _ingest/pipeline/indexed_at
{
  "description": "Adds indexed_at timestamp to documents",
  "processors": [
    {
      "set": {
        "field": "_source.indexed_at",
        "value": "{{_ingest.timestamp}}"
      }
    }
  ]
}
```
----
Add pipeline to index
``` bash
PUT /tags/_settings
{
  "index.default_pipeline": "indexed_at"
}
```
----
Scrolling API
``` bash
GET /tags/_search?scroll=1m&size=10
{
    "query": {
        "match" : {
            "name" : "John"
        }
    }
}
```
