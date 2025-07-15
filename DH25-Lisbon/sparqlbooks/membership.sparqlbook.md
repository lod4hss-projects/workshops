# Create memberships

```sparql
PREFIX wd: <http://www.wikidata.org/entity/>
PREFIX wdt: <http://www.wikidata.org/prop/direct/> 
PREFIX crm: <http://www.cidoc-crm.org/cidoc-crm/>

select * where {
            GRAPH <https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/graphs/wikidata-imported-data.md>
            {
            ?s a  wd:Q5;
                wdt:P463 ?organisation.
            
            }
}
ORDER BY ?s
limit 10


```

```sparql
PREFIX wd: <http://www.wikidata.org/entity/>
PREFIX crm: <http://www.cidoc-crm.org/cidoc-crm/>
PREFIX sdh-so: <https://ontome.net/ns/social-legal-economic-life/>
PREFIX wdt: <http://www.wikidata.org/prop/direct/>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>



CONSTRUCT {?id1 rdf:type sdh-so:C5;
                sdh-so:P1 ?pers;
                sdh-so:P2 ?org.
                }
WHERE {
    SELECT 
        ?pers ?org
        (URI(CONCAT('https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/resource/', STRUUID())) as ?id1) 
    WHERE         
        {
        SELECT DISTINCT ?pers ?org
        WHERE {
            GRAPH <https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/graphs/wikidata-imported-data.md>
            {
            ?s a  wd:Q5;
                wdt:P463 ?organisation.
            
            }
            GRAPH <https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/graphs/sdhss-data.md>
            {
            ?org owl:sameAs ?organisation.
            ?pers owl:sameAs ?s
            }
        }
        LIMIT 5
        }
}


```

```sparql
PREFIX wd: <http://www.wikidata.org/entity/>
PREFIX wdt: <http://www.wikidata.org/prop/direct/> 
PREFIX crm: <http://www.cidoc-crm.org/cidoc-crm/>
PREFIX sdh-so: <https://ontome.net/ns/social-legal-economic-life/>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

INSERT {GRAPH <https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/graphs/sdhss-data.md>
   		{?id1 rdf:type sdh-so:C5;
                sdh-so:P1 ?pers;
                sdh-so:P2 ?org.
                }
}
WHERE {
    SELECT 
        ?pers ?org
        (URI(CONCAT('https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/resource/', STRUUID())) as ?id1) 
    WHERE         
        {
        SELECT DISTINCT ?pers ?org
        WHERE {
            GRAPH <https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/graphs/wikidata-imported-data.md>
            {
            ?s a  wd:Q5;
                wdt:P463 ?organisation.
            
            }
            GRAPH <https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/graphs/sdhss-data.md>
            {
            ?org owl:sameAs ?organisation.
            ?pers owl:sameAs ?s
            }
        }
        LIMIT 5
        }
}


```
