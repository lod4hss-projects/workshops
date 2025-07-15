https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/resource/

<https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/graphs/sdhss-data.md>

<https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/graphs/wikidata-imported-data.md>
      

```sparql
### Content of the wikidata graph 

select ?s  ?p ?o
where {
    {
        GRAPH <https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/graphs/wikidata-imported-data.md>
        {
            ?s  ?p ?o.            
        }
    }
}
limit 10
```

```sparql
PREFIX wd: <http://www.wikidata.org/entity/>
PREFIX crm: <http://www.cidoc-crm.org/cidoc-crm/>

select * where {
    {
        GRAPH <https://github.com/Sciences-historiques-numeriques/astronomers/blob/main/graphs/wikidata-imported-data.md>{
            ?s  a  wd:Q5;
                rdfs:label ?label.
            
            }
    
  }
}
limit 10


```

```sparql
SELECT (URI(CONCAT('https://science-in-context.wisski.cloud/entity/', STRUUID())) as ?id1) {}
```

```sparql
PREFIX wd: <http://www.wikidata.org/entity/>
PREFIX crm: <http://www.cidoc-crm.org/cidoc-crm/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX base: <https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/resource/>

CONSTRUCT {?id1 rdf:type crm:E21;
                rdfs:label ?sLabel;
                owl:sameAs ?s.
                }
WHERE {
    {SELECT DISTINCT ?s ?sLabel
    (URI(CONCAT('https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/resource/', STRUUID())) as ?id1)
      WHERE {
        SELECT DISTINCT ?s ?sLabel
        WHERE {
        GRAPH <https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/graphs/wikidata-imported-data.md>
        {
            ?s  a  wd:Q5;
            rdfs:label ?sLabel.
                }
            }    
    }
    OFFSET 50
    LIMIT 3
    }
}


```

```sparql
PREFIX wd: <http://www.wikidata.org/entity/>
PREFIX crm: <http://www.cidoc-crm.org/cidoc-crm/>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX base: <https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/resource/>


INSERT {GRAPH <https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/graphs/sdhss-data.md>
    	{?id1 rdf:type crm:E21;
                rdfs:label ?sLabel;
                owl:sameAs ?s.
                }
}
WHERE {
    {SELECT DISTINCT ?s ?sLabel
    (URI(CONCAT('https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/resource/', STRUUID())) as ?id1)
      WHERE {
        SELECT DISTINCT ?s ?sLabel
        WHERE {
        GRAPH <https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/graphs/wikidata-imported-data.md>
        {
            ?s  a  wd:Q5;
            rdfs:label ?sLabel.
                }
            }    
    }
   }
}



```

```sparql

```

```sparql
PREFIX crm: <http://www.cidoc-crm.org/cidoc-crm/>
select ?s ?p ?o where {
    {
        GRAPH <https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/graphs/sdhss-data.md>
            {
                ?s  a crm:E21;
                    ?p ?o.
            }
    }
}
limit 10
```
#### Create the persons's appellations

    NOT YET IMPLEMENTED !

```sparql
PREFIX wd: <http://www.wikidata.org/entity/>
PREFIX crm: <http://www.cidoc-crm.org/cidoc-crm/>

CONSTRUCT {?s crm:P1_is_identified_by ?id1.    
           ?id1 rdf:type crm:E41_Appellation;
                crm:P3_has_note ?label.
                }
WHERE { 
        SELECT ?s ?label 
        (URI(CONCAT('https://science-in-context.wisski.cloud/entity/', STRUUID())) as ?id1)     
        WHERE 
        {
            SELECT DISTINCT ?s ?label
            WHERE {

                {
                    GRAPH <https://science-in-context.wisski.cloud/entity/>{        
                        ?s a crm:E21_Person;
                            owl:sameAs ?wdUri}
                }

                SERVICE <https://ag16gm9pr0meths2.allegrograph.cloud/repositories/astronomers>{
                GRAPH <https://github.com/Sciences-historiques-numeriques/astronomers/blob/main/graphs/wikidata-imported-data.md>{
                    ?wdUri rdfs:label ?wdLabel.
                
                    }
                }
                BIND(STR(?wdLabel) as ?label) 
            }
         }
           
        LIMIT 10
    
}


```

```sparql
PREFIX wd: <http://www.wikidata.org/entity/>
PREFIX crm: <http://www.cidoc-crm.org/cidoc-crm/>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

INSERT {GRAPH <https://science-in-context.wisski.cloud/entity/>
	{?s crm:P1_is_identified_by ?id1.    
           ?id1 rdf:type crm:E41_Appellation;
                crm:P3_has_note ?label.
                }
}
WHERE { 
        SELECT ?s ?label 
        (URI(CONCAT('https://science-in-context.wisski.cloud/entity/', STRUUID())) as ?id1)     
        WHERE 
        {
            SELECT DISTINCT ?s ?label
            WHERE {

                {
                    GRAPH <https://science-in-context.wisski.cloud/entity/>{        
                        ?s a crm:E21_Person;
                            owl:sameAs ?wdUri}
                }

                SERVICE <https://ag16gm9pr0meths2.allegrograph.cloud/repositories/astronomers>{
                GRAPH <https://github.com/Sciences-historiques-numeriques/astronomers/blob/main/graphs/wikidata-imported-data.md>{
                    ?wdUri rdfs:label ?wdLabel.
                
                    }
                }
                BIND(STR(?wdLabel) as ?label) 
            }
         }
}



```
### Add birth and birth date

```sparql
PREFIX wd: <http://www.wikidata.org/entity/>
PREFIX wdt: <http://www.wikidata.org/prop/direct/>
PREFIX crm: <http://www.cidoc-crm.org/cidoc-crm/>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT ?pUri ?birthDate
    (URI(CONCAT('https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/resource/', STRUUID())) as ?id1) 
    (URI(CONCAT('https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/resource/', STRUUID())) as ?id2) 
     WHERE {
        GRAPH <https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/graphs/wikidata-imported-data.md>
        {
            ?s  a  wd:Q5;
                wdt:P569 ?birthDate.
            }
        
        GRAPH <https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/graphs/sdhss-data.md>
        {
            ?pUri owl:sameAs ?s.    
            }
     }    
    ORDER BY ?pUri
    LIMIT 10
```

```sparql
PREFIX wd: <http://www.wikidata.org/entity/>
PREFIX wdt: <http://www.wikidata.org/prop/direct/>
PREFIX crm: <http://www.cidoc-crm.org/cidoc-crm/>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX sdh-short: <https://sdhss.org/ontology/shortcuts/>


CONSTRUCT {?id1 crm:P98 ?pUri;
                rdf:type crm:E67;
                sdh-short:P1 ?birthDate
                }
WHERE {
    {
    SELECT DISTINCT ?pUri (MAX(?birthDate) as ?birthDate)
    (URI(CONCAT('https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/resource/', STRUUID())) as ?id1) 
    WHERE {
        GRAPH <https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/graphs/wikidata-imported-data.md>
        {
            ?s  a  wd:Q5;
                wdt:P569 ?birthDate.
            }

            GRAPH <https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/graphs/sdhss-data.md>
            {        
                ?pUri owl:sameAs ?s.    
            }    
    }
    GROUP BY ?pUri
    ORDER BY ?pUri
    LIMIT 5

    }
}


```

```sparql
### Creates births and their (shortcut) dates 

PREFIX wd: <http://www.wikidata.org/entity/>
PREFIX wdt: <http://www.wikidata.org/prop/direct/>
PREFIX crm: <http://www.cidoc-crm.org/cidoc-crm/>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX sdh-short: <https://sdhss.org/ontology/shortcuts/>

INSERT {GRAPH <https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/graphs/sdhss-data.md>
            {?id1 crm:P98 ?pUri;
                rdf:type crm:E67;
                sdh-short:P1 ?birthDate
                }
        }
WHERE {
    {
    SELECT DISTINCT ?pUri (MAX(?birthDate) as ?birthDate)
    (URI(CONCAT('https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/resource/', STRUUID())) as ?id1) 
    WHERE {
        GRAPH <https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/graphs/wikidata-imported-data.md>
        {
            ?s  a  wd:Q5;
                wdt:P569 ?birthDate.
            }

            GRAPH <https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/graphs/sdhss-data.md>
            {        
                ?pUri owl:sameAs ?s.    
            }    
    }
    GROUP BY ?pUri
    ORDER BY ?pUri
    }
}



```

```sparql
### Number of births
PREFIX crm: <http://www.cidoc-crm.org/cidoc-crm/>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX sdh-short: <https://sdhss.org/ontology/shortcuts/>

SELECT (COUNT(*) as ?n)
WHERE {
            GRAPH <https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/graphs/sdhss-data.md>
            {        
                ?birth a crm:E67.    
            }    
}
```
### Get birth places

We add places to existings births, where dates are available. 

It is therefore possible that we miss some birth places without date, although in fact persons without birth date shouldn't be present

```sparql
PREFIX wd: <http://www.wikidata.org/entity/>
PREFIX wdt: <http://www.wikidata.org/prop/direct/>
PREFIX crm: <http://www.cidoc-crm.org/cidoc-crm/>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX sic:  <https://science-in-context.wisski.cloud/entity/>

SELECT ?pUri ?birth ?birthPlace
     WHERE {
        GRAPH <https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/graphs/wikidata-imported-data.md>{
            ?s  a  wd:Q5;
                wdt:P19 ?wdBirthPlace.
            }
        GRAPH <https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/graphs/sdhss-data.md>{
            ?pUri owl:sameAs ?s;
                 ^crm:P98 ?birth.
            ?birthPlace owl:sameAs ?wdBirthPlace.     
            }    
    }
    ORDER BY ?pUri
    LIMIT 10
```

```sparql
PREFIX wd: <http://www.wikidata.org/entity/>
PREFIX wdt: <http://www.wikidata.org/prop/direct/>
PREFIX crm: <http://www.cidoc-crm.org/cidoc-crm/>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX sic:  <https://science-in-context.wisski.cloud/entity/>
PREFIX sdh:  <https://sdhss.org/ontology/core/>

CONSTRUCT {?birth crm:P6 ?birthPlace.
                }
WHERE {
        GRAPH <https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/graphs/wikidata-imported-data.md>{
            ?s  a  wd:Q5;
                wdt:P19 ?wdBirthPlace.
            }
        GRAPH <https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/graphs/sdhss-data.md>{
            ?pUri owl:sameAs ?s;
                 ^crm:P98 ?birth.
            ?birthPlace owl:sameAs ?wdBirthPlace.     
            }    
    }
    ORDER BY ?pUri
    LIMIT 10


```

```sparql
PREFIX wd: <http://www.wikidata.org/entity/>
PREFIX wdt: <http://www.wikidata.org/prop/direct/>
PREFIX crm: <http://www.cidoc-crm.org/cidoc-crm/>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX sic:  <https://science-in-context.wisski.cloud/entity/>
PREFIX sdh:  <https://sdhss.org/ontology/core/>

INSERT {GRAPH <https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/graphs/sdhss-data.md>
 {?birth crm:P6 ?birthPlace.
                }
}
WHERE 
    {
    SELECT ?pUri ?birth ?birthPlace
    WHERE {
        GRAPH <https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/graphs/wikidata-imported-data.md>{
            ?s  a  wd:Q5;
                wdt:P19 ?wdBirthPlace.
            }
        GRAPH <https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/graphs/sdhss-data.md>{
            ?pUri owl:sameAs ?s;
                 ^crm:P98 ?birth.
            ?birthPlace owl:sameAs ?wdBirthPlace.     
            }    
    }
}


```
