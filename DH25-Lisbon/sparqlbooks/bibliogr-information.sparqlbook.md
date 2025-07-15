

```sparql
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>


SELECT  ?class ?cLabel (COUNT(*) as ?n)
WHERE {
    GRAPH <https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/graphs/idref-sudoc.md>
    {
    ?s a ?class.
    OPTIONAL {?class rdfs:label ?cLabel}
    }
}
GROUP BY ?class ?cLabel
```
http://purl.org/ontology/bibo/Book

```sparql
### Count properties' occurrencies in the repository

PREFIX franzOption_defaultDatasetBehavior: <franz:rdf>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX wdt: <http://www.wikidata.org/prop/direct/>

SELECT ?p ?pLabel (COUNT(*) AS ?n)
WHERE {
    GRAPH <https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/graphs/idref-sudoc.md>
    {
        ?s ?p ?o.
        OPTIONAL {?p rdfs:label ?pLabel}
    }
}
GROUP BY ?p ?pLabel
ORDER BY DESC(?n)
```

```sparql
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX wdt: <http://www.wikidata.org/prop/direct/>

select ?s  ?o
where {
    {
        GRAPH <https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/graphs/wikidata-imported-data.md>
        {
            ?s wdt:P269 ?o.
        }
    }
}
limit 10
```

```sparql
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

```sparql
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX wdt: <http://www.wikidata.org/prop/direct/>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX sdh-short: <https://sdhss.org/ontology/shortcuts/>
PREFIX crm: <http://www.cidoc-crm.org/cidoc-crm/>
PREFIX crm-sup: <https://sdhss.org/ontology/crm-supplement/>
PREFIX sdh-info: <https://sdhss.org/ontology/sources-information-metadata/>
PREFIX frbroo: <http://iflastandards.info/ns/fr/frbr/frbroo/>

CONSTRUCT { ?id1 a sdh-info:C1;
                sdh-short:P1 ?date;
                sdh-info:P3 ?pUri;
                sdh-info:P2 ?id2.
            ?id2 owl:sameAs ?book;
                  crm:P1 ?id3.
            ?id3 a sdh-info:C5;
                  rdfs:label ?bibliogRef.
}
where {
    SELECT 
        ?pUri  ?bibliogRef ?date ?book
        (URI(CONCAT('https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/resource/', STRUUID())) as ?id1) 
        (URI(CONCAT('https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/resource/', STRUUID())) as ?id2) 
        (URI(CONCAT('https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/resource/', STRUUID())) as ?id3) 
    WHERE         
        {
            SELECT DISTINCT ?pUri  ?bibliogRef ?date ?book
            WHERE {
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
                        
                }
            }
            OFFSET 100
            LIMIT 3
        }    
}

```

```sparql
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX wdt: <http://www.wikidata.org/prop/direct/>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX sdh-short: <https://sdhss.org/ontology/shortcuts/>
PREFIX crm: <http://www.cidoc-crm.org/cidoc-crm/>
PREFIX crm-sup: <https://sdhss.org/ontology/crm-supplement/>
PREFIX sdh-info: <https://sdhss.org/ontology/sources-information-metadata/>
PREFIX frbroo: <http://iflastandards.info/ns/fr/frbr/frbroo/>

INSERT { 
    GRAPH <https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/graphs/sdhss-data.md>
    { ?id1 a sdh-info:C1;
                sdh-short:P1 ?date;
                sdh-info:P3 ?pUri;
                sdh-info:P2 ?id2.
            ?id2 owl:sameAs ?book;
                  crm:P1 ?id3.
            ?id3 a sdh-info:C5;
                  rdfs:label ?bibliogRef.
    }              
}
where {
    SELECT 
        ?pUri  ?bibliogRef ?date ?book
        (URI(CONCAT('https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/resource/', STRUUID())) as ?id1) 
        (URI(CONCAT('https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/resource/', STRUUID())) as ?id2) 
        (URI(CONCAT('https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/resource/', STRUUID())) as ?id3) 
    WHERE         
        {
            SELECT DISTINCT ?pUri  ?bibliogRef ?date ?book
            WHERE {
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
                }
            }
        }    
}

```
### Label and class added to created books

```sparql
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX sdh-short: <https://sdhss.org/ontology/shortcuts/>
PREFIX crm: <http://www.cidoc-crm.org/cidoc-crm/>
PREFIX crm-sup: <https://sdhss.org/ontology/crm-supplement/>
PREFIX sdh-info: <https://sdhss.org/ontology/sources-information-metadata/>
PREFIX frbroo: <http://iflastandards.info/ns/fr/frbr/frbroo/>

SELECT ?book ?biblioRef ?biblioRefLabel
WHERE {
      GRAPH <https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/graphs/sdhss-data.md>
            { ?book crm:P1 ?biblioRef.
           ?biblioRef a sdh-info:C5;
            rdfs:label ?biblioRefLabel.
            }              
}
LIMIT 10
```

```sparql
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX sdh-short: <https://sdhss.org/ontology/shortcuts/>
PREFIX crm: <http://www.cidoc-crm.org/cidoc-crm/>
PREFIX crm-sup: <https://sdhss.org/ontology/crm-supplement/>
PREFIX sdh-info: <https://sdhss.org/ontology/sources-information-metadata/>
PREFIX frbroo: <http://iflastandards.info/ns/fr/frbr/frbroo/>

CONSTRUCT { ?book a frbroo:F3;
                  rdfs:label ?biblioRefLabel}
WHERE {
      GRAPH <https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/graphs/sdhss-data.md>
            { ?book crm:P1 ?biblioRef.
           ?biblioRef a sdh-info:C5;
            rdfs:label ?biblioRefLabel.
            }              
}
LIMIT 10
```

```sparql
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX sdh-short: <https://sdhss.org/ontology/shortcuts/>
PREFIX crm: <http://www.cidoc-crm.org/cidoc-crm/>
PREFIX crm-sup: <https://sdhss.org/ontology/crm-supplement/>
PREFIX sdh-info: <https://sdhss.org/ontology/sources-information-metadata/>
PREFIX frbroo: <http://iflastandards.info/ns/fr/frbr/frbroo/>

INSERT  { GRAPH <https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/graphs/sdhss-data.md>
      {?book a frbroo:F3;
                  rdfs:label ?biblioRefLabel
                  }
                  }
WHERE {
      GRAPH <https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/graphs/sdhss-data.md>
            { ?book crm:P1 ?biblioRef.
           ?biblioRef a sdh-info:C5;
            rdfs:label ?biblioRefLabel.
            }              
}

```
