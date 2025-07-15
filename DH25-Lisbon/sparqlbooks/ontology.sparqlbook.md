# Inspect the SHACL profiles


```sparql

#PREFIX franzOption_defaultDatasetBehavior: <franz:rdf>
PREFIX sh: <http://www.w3.org/ns/shacl#>
PREFIX wd: <http://www.wikidata.org/entity/>


# View unique named graphs
SELECT DISTINCT ?sh ?description ?class ?classLabel   ?property ?propertyLabel ?targetClass ?targetClassLabel  ?datatype ?g

WHERE
{ graph 
 # ?g
 <https://github.com/lod4hss-projects/workshops/blob/main/DH25-Lisbon/graphs/sdhss-shacl.md>
 {
 { ?sh sh:targetClass ?class;
    sh:name ?classLabel;
  sh:property ?sh_p.
  OPTIONAL {?sh sh:description ?description}
  ?sh_p sh:path ?property;
    sh:class ?targetClass;
    sh:name ?targetClassLabel.
  OPTIONAL{ ?sh_p sh:name ?propertyLabel}
  }
 UNION
 # datatype properties
 { ?sh sh:targetClass ?class;
    sh:name ?classLabel;
    sh:property ?sh_p1.
    OPTIONAL {?sh sh:description ?description}
  ?sh_p1 sh:path ?property;
  sh:datatype ?datatype.
 OPTIONAL{ ?sh_p1 sh:name ?propertyLabel}
  }
   }
 }
order by ?g ?sh ?property





```
