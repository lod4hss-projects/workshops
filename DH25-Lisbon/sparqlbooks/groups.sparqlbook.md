## Add groups (organisations)

```sparql
PREFIX wd: <http://www.wikidata.org/entity/>
PREFIX crm: <http://www.cidoc-crm.org/cidoc-crm/>

SELECT DISTINCT ?s ?label where {
    {
        GRAPH <https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/graphs/wikidata-imported-data.md>
        {
            ?s  a  crm:E74_Group;
                rdfs:label ?wdLabel.
            
            }
    }
    BIND(STR(?wdLabel) as ?label)
}
limit 5


```

```sparql
SELECT (URI(CONCAT('https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/resource/', STRUUID())) as ?id1) {}
```

```sparql
PREFIX wd: <http://www.wikidata.org/entity/>
PREFIX crm: <http://www.cidoc-crm.org/cidoc-crm/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

CONSTRUCT {?id1 rdf:type crm:E74;
                owl:sameAs ?s;
                rdfs:label ?wdLabel.
                }
where {
    SELECT ?s ?wdLabel
    (URI(CONCAT('https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/resource/', STRUUID())) as ?id1) 
    WHERE
    {SELECT DISTINCT ?s ?wdLabel
     WHERE {
        GRAPH <https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/graphs/wikidata-imported-data.md>
        {
            ?s  a  crm:E74_Group;
                rdfs:label ?wdLabel.
            
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
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

INSERT {GRAPH <https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/graphs/sdhss-data.md>
   		 {?id1 rdf:type crm:E74;
                owl:sameAs ?s;
                rdfs:label ?wdLabel.
                }
        }
where {
    SELECT ?s ?wdLabel
    (URI(CONCAT('https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/resource/', STRUUID())) as ?id1) 
    WHERE
    {SELECT DISTINCT ?s ?wdLabel
     WHERE {
        GRAPH <https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/graphs/wikidata-imported-data.md>
        {
            ?s  a  crm:E74_Group;
                rdfs:label ?wdLabel.
            
            }
     }    
    }
}




```

```sparql
PREFIX wd: <http://www.wikidata.org/entity/>
PREFIX wdt: <http://www.wikidata.org/prop/direct/> 
PREFIX crm: <http://www.cidoc-crm.org/cidoc-crm/>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT ?sLabel ?s ?swd 
where {
GRAPH <https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/graphs/sdhss-data.md>
   		 {?s rdf:type crm:E74;
                owl:sameAs ?swd;
                rdfs:label ?sLabel.
                }
        }
OFFSET 500
LIMIT 5        
```

```sparql

```
### Get group labels


**NOT IMPLEMENTED YET !**
Attention dans les données il y a une erreur dans le label à : "Sewanee: The University of the South"

Le prend donc pour un URI !


http://www.wikidata.org/entity/Q7458159


Manquent les double-quotes dans le RDF de Wikidata.


Trouvé grâce à:
```
ORDER BY ?s
OFFSET 7545
```


**Correction**: j'ajoute un BIND / STR supplémentaire


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
                        ?s a crm:E74_Group;
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
           
        LIMIT 3
    
}


```

```sparql
PREFIX wd: <http://www.wikidata.org/entity/>
PREFIX wdt: <http://www.wikidata.org/prop/direct/> 
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
                        ?s a crm:E74_Group;
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

```sparql

```

```sparql
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX wd: <http://www.wikidata.org/entity/>
PREFIX crm: <http://www.cidoc-crm.org/cidoc-crm/>

SELECT ?s ?p ?o
WHERE { GRAPH <https://science-in-context.wisski.cloud/entity/>
{
?s rdf:type crm:E74_Group;
   ?p ?o.
}
}
LIMIT 10
	

```
### Archives: correction données en trop

```sparql
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX crm: <http://www.cidoc-crm.org/cidoc-crm/>
delete {?s ?p ?o}
where {
    GRAPH <https://science-in-context.wisski.cloud/entity/>{
    ?s owl:sameAs <http://www.wikidata.org/entity/Q7458159>;
    ?p ?o.
    # ?s crm:P1_is_identified_by ?label
    MINUS {?s crm:P1_is_identified_by ?label}
} }

```

```sparql
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX crm: <http://www.cidoc-crm.org/cidoc-crm/>
delete {?s ?p ?o}
where {
    GRAPH <https://science-in-context.wisski.cloud/>{
    ?s ?p ?o.
    # ?s crm:P1_is_identified_by ?label
    MINUS {?s crm:P1_is_identified_by ?label}
} }

```

```sparql
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX crm: <http://www.cidoc-crm.org/cidoc-crm/>
delete {?s ?p ?o}
where {
    GRAPH <https://science-in-context.wisski.cloud/>{
    ?s ?p ?o;
        rdf:type crm:E74_Group;
    crm:P1_is_identified_by ?app.
        
    MINUS {?app ?p1 ?o1.}
} }

```

```sparql

```
