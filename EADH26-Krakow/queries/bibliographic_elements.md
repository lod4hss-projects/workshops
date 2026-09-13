# Bibliographic Information Queries

Here are the list of queries for finding all of the persons and there respective publications

## Finding the list of persons in the SDHSS information graph

```
PREFIX crm:  <http://www.cidoc-crm.org/cidoc-crm/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT ?pUri ?pLabel
WHERE {
  GRAPH <https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/graphs/sdhss-data.md> {
    ?pUri a crm:E21 ;
          rdfs:label ?pLabel .
  }
}
LIMIT 10
```

## Find the equivalent wikidata instances URI of those persons

```
PREFIX crm:  <http://www.cidoc-crm.org/cidoc-crm/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT ?pUri ?pLabel ?wdUri
WHERE {
  GRAPH <https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/graphs/sdhss-data.md> {
    ?pUri a crm:E21 ;
        rdfs:label ?pLabel ;
        owl:sameAs ?wdUri
  }
}
LIMIT 10
```

## Finding in the equivalent IdRef URI from the Wikidata graph

```
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX wdt: <http://www.wikidata.org/prop/direct/>
PREFIX crm:  <http://www.cidoc-crm.org/cidoc-crm/>

select ?pUri  ?pLabel ?wdUri ?idref
where {
    {
        GRAPH <https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/graphs/sdhss-data.md>
        {
        ?pUri a crm:E21 ;
            rdfs:label ?pLabel ;
            owl:sameAs ?wdUri

        }
        GRAPH <https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/graphs/wikidata-imported-data.md>
        {
            ?wdUri wdt:P269 ?idref.
        }
    }
}
limit 10
```

## Querying the persons in the sdhss-info graph, their equivalent instances in the wikidata and idref graphs, and the bibliographic informations in the SUDOC
```
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX wdt: <http://www.wikidata.org/prop/direct/>

select ?pUri  ?bibliogRef ?date ?book 
where {
    {
        GRAPH <https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/graphs/wikidata-imported-data.md>
        {
            ?s wdt:P269 ?idref.
        }
        GRAPH <https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/graphs/sdhss-data.md>
        {
            ?pUri owl:sameAs ?s.
        }
        GRAPH <https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/graphs/idref-sudoc.md>
        {  ?book <http://id.loc.gov/vocabulary/relators/aut> ?idref;
                a <http://purl.org/ontology/bibo/Book>;
                <http://purl.org/dc/terms/bibliographicCitation> ?bibliogRef;
                <http://purl.org/dc/elements/1.1/date> ?date
        }
    
    BIND(URI(CONCAT('https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/resource/', STRUUID())) as ?id1) 

    }
}
limit 10
```
