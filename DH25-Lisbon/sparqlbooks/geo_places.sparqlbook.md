
```sparql

```

```sparql

```

```sparql
PREFIX wd: <http://www.wikidata.org/entity/>
PREFIX wdt: <http://www.wikidata.org/prop/direct/>
PREFIX crm: <http://www.cidoc-crm.org/cidoc-crm/>
PREFIX sdh: <https://sdhss.org/ontology/core/>
PREFIX base: <https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/graphs/>

SELECT ?place (MIN(?label) AS ?label) 
        (MIN(?geoCoordinates) AS ?geoCoordinates) 
WHERE {
        GRAPH base:wikidata-imported-data.md
            {
            ?place rdf:type sdh:C13;
                       rdfs:label  ?placeLabel;
                       wdt:P625 ?coordinates.
            
            }
    
    BIND(STR(?placeLabel) as ?label)
    BIND(Replace(?coordinates, 'Point', 'POINT') as ?geoCoordinates)

}
GROUP BY ?place
limit 10


```

```sparql
SELECT (URI(CONCAT('https://science-in-context.wisski.cloud/', STRUUID())) as ?id1) {}
```

```sparql
PREFIX wd: <http://www.wikidata.org/entity/>
PREFIX wdt: <http://www.wikidata.org/prop/direct/>
PREFIX crm: <http://www.cidoc-crm.org/cidoc-crm/>
PREFIX sdh: <https://sdhss.org/ontology/core/>

CONSTRUCT {?id1 rdf:type sdh:C13;
                owl:sameAs ?place;
                crm:P1 ?id2.    
           ?id2 rdf:type crm:E41;
                rdfs:label ?label.
                }
where {
    SELECT ?place ?label ?geoCoordinates
    (URI(CONCAT('https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/resource/', STRUUID())) as ?id1) 
    (URI(CONCAT('https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/resource/', STRUUID())) as ?id2) 
    WHERE
    {
        SELECT ?place (MIN(?label) AS ?label) 
                (MIN(?geoCoordinates) AS ?geoCoordinates) 
        WHERE {
            {
                GRAPH <https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/graphs/wikidata-imported-data.md>
                  {
            ?place rdf:type sdh:C13;
                       rdfs:label  ?placeLabel;
                       wdt:P625 ?coordinates.
            
            }
    
            }
            BIND(STR(?placeLabel) as ?label)
            BIND(REPLACE(?coordinates, 'Point', 'POINT') as ?geoCoordinates)

        }
        GROUP BY ?place
        offset 100
        LIMIT 3
    }
}


```

```sparql

```

```sparql

```

```sparql
### Test value type conversion

PREFIX crm: <http://www.cidoc-crm.org/cidoc-crm/>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX geo: <http://www.opengis.net/ont/geosparql#>
PREFIX ogc: <http://www.opengis.net/ont/geosparql#> 
select ?geo where {
    graph <https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/resource/>
    {?s crm:P168_place_is_defined_by ?geo .
    BIND(STR(?geo)^^geo:wktLiteral as ?out)
        
    }
} 
limit 10

```

```sparql
### Test value type conversion

PREFIX crm: <http://www.cidoc-crm.org/cidoc-crm/>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX geo: <http://www.opengis.net/ont/geosparql#>
PREFIX ogc: <http://www.opengis.net/ont/geosparql#> 
select ?geo (STR(?geo)^^geo:wktLiteral as ?out)
where {
    graph <https://science-in-context.wisski.cloud/entity/>
    {?s crm:P168_place_is_defined_by ?geo .
    # BIND(STR(?geo)^^geo:wktLiteral as ?out)
        
    }
} 
limit 10

```

```sparql
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> 
PREFIX ogc: <http://www.opengis.net/ont/geosparql#> 
select ?out
    where {
   #Bind("POINT(48.5 11.7)"^^ogc:wktLiteral as ?out)
   BIND("POINT(13.345242 50.6564031)"^^ogc:wktLiteral as ?out) 

} 
```

```sparql
PREFIX wd: <http://www.wikidata.org/entity/>
PREFIX wdt: <http://www.wikidata.org/prop/direct/>
PREFIX crm: <http://www.cidoc-crm.org/cidoc-crm/>
PREFIX sdh: <https://sdhss.org/ontology/core/>
PREFIX ogc: <http://www.opengis.net/ont/geosparql#> 

CONSTRUCT {?id1 rdf:type sdh:C13;
                rdfs:label ?label;
                owl:sameAs ?place.    
           ?id2 rdf:type crm:E93;
                crm:P167 ?id3;
                crm:P166 ?id1.
           ?id3 rdf:type crm:E53;
                crm:P168 ?geoCoordinates
                }
WHERE {
    SELECT ?place ?label ?geoCoordinates
    (URI(CONCAT('https://science-in-context.wisski.cloud/entity/', STRUUID())) as ?id1) 
    (URI(CONCAT('https://science-in-context.wisski.cloud/entity/', STRUUID())) as ?id2)
    (URI(CONCAT('https://science-in-context.wisski.cloud/entity/', STRUUID())) as ?id3)      
    WHERE
    {
        SELECT ?place (MIN(?label) AS ?label)
            (STRDT(MIN(?geoCoordinates),ogc:wktLiteral) AS ?geoCoordinates) 
        WHERE {
            {
                 GRAPH <https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/graphs/wikidata-imported-data.md>
                 {
                    ?place rdf:type sdh:C13;
                            rdfs:label  ?placeLabel;
                            wdt:P625 ?coordinates.
                    
                    } 
            }
            BIND(STR(?placeLabel) as ?label)
            BIND(REPLACE(?coordinates, 'Point', 'POINT') as ?geoCoordinates)

        }
        GROUP BY ?place
        LIMIT 5
    }
}


```

```sparql
PREFIX wd: <http://www.wikidata.org/entity/>
PREFIX wdt: <http://www.wikidata.org/prop/direct/>
PREFIX crm: <http://www.cidoc-crm.org/cidoc-crm/>
PREFIX sdh: <https://sdhss.org/ontology/core/>
PREFIX ogc: <http://www.opengis.net/ont/geosparql#> 

INSERT {GRAPH <https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/graphs/sdhss-data.md>
        {?id1 rdf:type sdh:C13;
                rdfs:label ?label;
                owl:sameAs ?place.    
           ?id2 rdf:type crm:E93;
                crm:P167 ?id3;
                crm:P166 ?id1.
           ?id3 rdf:type crm:E53;
                crm:P168 ?geoCoordinates
                }
    }       
WHERE {
    SELECT ?place ?label ?geoCoordinates
    (URI(CONCAT('https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/resource/', STRUUID())) as ?id1) 
    (URI(CONCAT('https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/resource/', STRUUID())) as ?id2)
    (URI(CONCAT('https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/resource/', STRUUID())) as ?id3)      
    WHERE
    {
        SELECT ?place (MIN(?label) AS ?label) 
                #(MIN(?geoPoint) AS ?geoCoordinates) 
                (STRDT(MIN(?geoPoint),ogc:wktLiteral) AS ?geoCoordinates) 
        WHERE {
            {
                GRAPH <https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/graphs/wikidata-imported-data.md>
                     {
                        ?place rdf:type sdh:C13;
                                rdfs:label  ?placeLabel;
                                wdt:P625 ?coordinates.
                    
                    }    
            }
            BIND(STR(?placeLabel) as ?label)
            BIND(REPLACE(?coordinates, 'Point', 'POINT') as ?geoPoint)

        }
        GROUP BY ?place
    }
}


```

```sparql
### Values corrected after first insert

prefix crm: <http://www.cidoc-crm.org/cidoc-crm/>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
prefix geo: <http://www.opengis.net/ont/geosparql#>
PREFIX ogc: <http://www.opengis.net/ont/geosparql#> 

DELETE { 
    GRAPH <https://science-in-context.wisski.cloud/entity/>
    {?s crm:P168_place_is_defined_by ?geo.}
	}
INSERT {
    GRAPH <https://science-in-context.wisski.cloud/entity/>
    {?s crm:P168_place_is_defined_by ?out.}
}
WHERE {
    GRAPH <https://science-in-context.wisski.cloud/entity/>
    {?s crm:P168_place_is_defined_by ?geo .
       BIND(STRDT(?geo,geo:wktLiteral) as ?out)
        
    }
} 


```

```sparql
### Property URI corrected after insert

prefix crm: <http://www.cidoc-crm.org/cidoc-crm/>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
prefix geo: <http://www.opengis.net/ont/geosparql#>
PREFIX ogc: <http://www.opengis.net/ont/geosparql#> 

DELETE { 
    GRAPH <https://science-in-context.wisski.cloud/entity/>
    {?s crm:P167_was_at ?geo.}
	}
INSERT {
    GRAPH <https://science-in-context.wisski.cloud/entity/>
    {?s crm:P167_was_within ?geo.}
}
WHERE {
    GRAPH <https://science-in-context.wisski.cloud/entity/>
    {?s crm:P167_was_at ?geo .}
} 


```
