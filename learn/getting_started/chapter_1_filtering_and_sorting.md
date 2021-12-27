# Chapter 1: Filtering and sorting

## Filtering

MeiliSearch allows you to refine your search using filters. You can use any of the document fields for filtering by adding them to `filterableAttributes`.

Let's say you only want to view meteors that weigh less than 200g.

<CodeSamples id= "getting_started_filtering_md" />

```json
{
  "hits":[
    {
      "name":"Aachen",
      "mass":21
    },
    {
      "name":"Emmaville",
      "mass":127
    },
    …
  ],
  "nbHits":114,
  "exhaustiveNbHits":false,
  "query":"",
  "limit":20,
  "offset":0,
  "processingTimeMs":0
}
```

## Sorting

By default, MeiliSearch focuses on ordering results according to their relevancy. You can alter this sorting behavior so users can decide at search time what type of results they want to see first.

You can use any of the document fields as long as they contain numbers, strings, arrays of numeric values, or arrays of string values by adding them to `sortableAttributes`. Let's sort the meteors in the previous example  based on mass.

<CodeSamples id= "getting_started_sorting_md" />

```json
{
  "hits":[
    {
      "name":"Silistra",
      "mass":0.15
    },
    {
      "name":"Hachi-oji",
      "mass":0.2
    },
    …
  ],
  "nbHits":114,
  "exhaustiveNbHits":false,
  "query":"",
  "limit":20,
  "offset":0,
  "processingTimeMs":1
  }
```

You will see all meteors weighing less than 200g sorted based on increasing mass. If you use `mass:desc`, MeiliSearch will sort them based on decreasing mass.

To learn more about `sortableAttributes` and how to configure them, refer to our [dedicated guide](/reference/features/sorting.md).

## Geosearch

MeiliSearch allows you to filter and sort results based on their geographic location. To use this feature, your documents need to have the `_geo` field.

Let's say you want to find out the what meteors crashed within a 210km radius of Bern:

<CodeSamples id= "getting_started_geoRadius_md" />

```json
{
  "hits":[
  {
    "name":"Ensisheim",
    "id":"10039",
    "nametype":"Valid",
    "recclass":"LL6",
    "mass":"127000",
    "fall":"Fell",
    "year":"1492-01-01T00:00:00.000",
    "_geo": {
        "lat":47.86667,
        "lng":7.35
        }
  },
  {
    "name":"Épinal",
    "id":"10041",
    "nametype":"Valid",
    "recclass":"H5",
    "mass":"277",
    "fall":"Fell",
    "year":"1822-01-01T00:00:00.000",
    "_geo": {
        "lat":48.18333,
        "lng":6.46667
        }
  },
  …
  ],
  "nbHits":7,
  "exhaustiveNbHits":false,
  "query":"",
  "limit":20,
  "offset":0,
  "processingTimeMs":3
  }
  ```

You can also use geosearch to sort results based on their distance from a specific location. Let's say you want to view meteors based on how close they were to the Taj Mahal:

<CodeSamples id= "getting_started_geoPoint_md" />

```json
{
  "hits":[
  {
    "name":"Nagaria",
    "id":"16892",
    "nametype":"Valid",
    "recclass":"Eucrite-cm",
    "mass":"20",
    "fall":"Fell",
    "year":"1875-01-01T00:00:00.000",
    "_geo": {
      "lat":26.98333,
      "lng":78.21667
      },
      "_geoDistance":27449
  },
  {
    "name":"Kheragur",
    "id":"12294",
    "nametype":"Valid",
    "recclass":"L6",
    "mass":"450",
    "fall":"Fell",
    "year":"1860-01-01T00:00:00.000",
    "_geo": {
      "lat":26.95,
      "lng":77.88333
      },
      "_geoDistance":29558
    },
  …
  ]
  "nbHits":1000,
  "exhaustiveNbHits":false,
  "query":"",
  "limit":20,
  "offset":0,
  "processingTimeMs":4
  }
```

This response returns an additional `_geoDistance` field. `_geoDistance` represents the distance between the Taj Mahal and each meteor in meters.

To learn more about geosearch and how to configure it, refer to our [dedicated guide](/reference/features/geosearch.md).