# Inspect available information in your repository

```sparql
### Count instances of 'classes' in the repository

PREFIX franzOption_defaultDatasetBehavior: <franz:rdf>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>

SELECT ?class ?classLabel (COUNT(*) AS ?n)
WHERE {
    GRAPH <https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/graphs/sdhss-data.md>
   
    {
        ?s rdf:type ?class.
        OPTIONAL {?class rdfs:label ?classLabel}
    }
}
GROUP BY ?class ?classLabel
ORDER BY DESC(?n)
```

```sparql
### Count properties' occurrencies in the repository

PREFIX franzOption_defaultDatasetBehavior: <franz:rdf>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX wdt: <http://www.wikidata.org/prop/direct/>

SELECT ?p ?pLabel (COUNT(*) AS ?n)
WHERE {
    GRAPH <https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/graphs/sdhss-data.md>
{
        ?s ?p ?o.
        OPTIONAL {?p rdfs:label ?pLabel}
    }
}
GROUP BY ?p ?pLabel
ORDER BY DESC(?n)
```
## Specific aspects

```sparql
PREFIX crm: <http://www.cidoc-crm.org/cidoc-crm/>
PREFIX sdh: <https://sdhss.org/ontology/core/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT DISTINCT (MAX(?placeLabel) as ?place) (COUNT(*) as ?number)
WHERE {
    GRAPH <https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/graphs/sdhss-data.md>
   {
    ?birth sdh:P6 ?geoPlace.
    ?geoPlace rdfs:label ?placeLabel
   }
}
GROUP BY ?geoPlace ?placeLabel
ORDER BY DESC(?number)
LIMIT 10
```

```sparql
    PREFIX crm: <http://www.cidoc-crm.org/cidoc-crm/>
    PREFIX sdh: <https://sdhss.org/ontology/core/>
    PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
    PREFIX sdh-slc: <https://sdhss.org/ontology/social-life/>

    SELECT  (MAX(?groupLabel) as ?group)  (COUNT(*) as ?number)
    WHERE {
        GRAPH <https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/graphs/sdhss-data.md>
    {
        ?membership sdh-slc:P2 ?groupUri.
        ?groupUri rdfs:label ?groupLabel
    }
    }
    GROUP BY ?groupUri # ?groupLabel
    ORDER BY DESC(?number)
    LIMIT 20
```
