---
layout: single
title: Elasticsearch cheatsheet
author: aNNufriy
tags: [elasticsearch]
cover_url: "/images/jekyll.png"
---

## Elasticsearch cheatsheet

<details><summary>Create index</summary>
<div markdown="1">
```bash
PUT /tags
```
</div>
</details>
----

<details><summary>Create pipeline</summary>
<div markdown="1">
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
</div>
</details>
----
<details><summary>Add pipeline to index</summary>
<div markdown="1">
``` bash
PUT /tags/_settings
{
  "index.default_pipeline": "indexed_at"
}
```
</div>
</details>
----

<details><summary>Scrolling API</summary>
<div markdown="1">
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
</div>
