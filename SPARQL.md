## Statistics

The results of these queries were computed over the whole [dataset](https://w3id.org/knowhow/dataset) (loaded on Virtuoso 07.20.3215).

 Query Number | Statistic | Value 
----|----|-----
1 | Number of triples | 23,033,490 | 
2 | Number labelled nodes | 2,610,223 |
3 | Number of main processes | 215,959 |

## Sample Endpoint

You can try some of these queries at the [Dydra public endpoint](https://w3id.org/knowhow/sparql). For federated queries, use [this URI](http://dydra.com/paolo-pareti/knowhow6/sparql). 

**NOTE**: this endpoint **does not** expose the whole dataset! Some query results might be missing or incomplete.

## Query Prefixes

Standard prefixes for all the queries:
```
PREFIX prohow: <http://w3id.org/prohow#> 
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> 
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> 
PREFIX oa: <http://www.w3.org/ns/oa#> 
PREFIX owl: <http://www.w3.org/2002/07/owl#> 
```

## Queries

Query 1) Count the number of triples. [Try it!](https://w3id.org/knowhow/sparql?query=SELECT+%28COUNT%28%2A%29+AS+%3Fno%29+WHERE+%7B+%3Fs+%3Fp+%3Fo++%7D)
```
SELECT (COUNT(*) AS ?no) WHERE { ?s ?p ?o  }
```
Query 2) Count the number of entities with an associated label. [Try it!](https://w3id.org/knowhow/sparql?query=PREFIX+prohow%3A+%3Chttp%3A%2F%2Fw3id.org%2Fprohow%23%3E+%0D%0APREFIX+rdf%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F1999%2F02%2F22-rdf-syntax-ns%23%3E+%0D%0APREFIX+rdfs%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23%3E+%0D%0APREFIX+oa%3A+%3Chttp%3A%2F%2Fwww.w3.org%2Fns%2Foa%23%3E+%0D%0A%0D%0ASELECT+%28COUNT%28distinct+%3Fs%29+AS+%3Fno%29+WHERE+%7B+%3Fs+rdfs%3Alabel+%3Fo++%7D)
```
SELECT (COUNT(distinct ?s) AS ?no) WHERE { ?s rdfs:label ?o  }
```
Query 3) Count of number of distinct sets of instructions. [Try it!](https://w3id.org/knowhow/sparql?query=PREFIX+prohow%3A+%3Chttp%3A%2F%2Fw3id.org%2Fprohow%23%3E+%0D%0APREFIX+rdf%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F1999%2F02%2F22-rdf-syntax-ns%23%3E+%0D%0APREFIX+rdfs%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23%3E+%0D%0APREFIX+oa%3A+%3Chttp%3A%2F%2Fwww.w3.org%2Fns%2Foa%23%3E+%0D%0A%0D%0ASELECT+%28COUNT%28distinct+%3Fmain%29+AS+%3Fno%29+WHERE+%7B+%3Fmain+rdf%3Atype+prohow%3Ainstruction_set+%7D)
```
SELECT (COUNT(distinct ?main) AS ?no) WHERE { ?main rdf:type prohow:instruction_set }
 ```
 Query 4) Search main sets of instructions that contain substring "email account" in the label. [Try it!](https://w3id.org/knowhow/sparql?query=PREFIX+prohow%3A+%3Chttp%3A%2F%2Fw3id.org%2Fprohow%23%3E+%0D%0APREFIX+rdf%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F1999%2F02%2F22-rdf-syntax-ns%23%3E+%0D%0APREFIX+rdfs%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23%3E+%0D%0APREFIX+oa%3A+%3Chttp%3A%2F%2Fwww.w3.org%2Fns%2Foa%23%3E+%0D%0A%0D%0ASELECT+%3Fmain+%3Flabel+WHERE+%7B+%0D%0A++%3Fmain+rdf%3Atype+prohow%3Ainstruction_set+.%0D%0A++%3Fmain+rdfs%3Alabel+%3Flabel+%0D%0A++FILTER+regex%28str%28%3Flabel%29%2C+%22email+account%22%2C+%22i%22+%29%0D%0A%7D+LIMIT+100)
 ```
SELECT ?main ?label WHERE { 
  ?main rdf:type prohow:instruction_set .
  ?main rdfs:label ?label 
  FILTER regex(str(?label), "email account", "i" )
} LIMIT 100
```
Query 5) Get the title and types (categories) of a set of instructions. [Try it!](https://w3id.org/knowhow/sparql?query=PREFIX+prohow%3A+%3Chttp%3A%2F%2Fw3id.org%2Fprohow%23%3E+%0D%0APREFIX+rdf%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F1999%2F02%2F22-rdf-syntax-ns%23%3E+%0D%0APREFIX+rdfs%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23%3E+%0D%0APREFIX+oa%3A+%3Chttp%3A%2F%2Fwww.w3.org%2Fns%2Foa%23%3E+%0D%0A%0D%0ASELECT+%3Flabel+%3Ftype+WHERE+%7B+%0D%0A++%3Chttp%3A%2F%2Fvocab.inf.ed.ac.uk%2Fprocont%23%3Furl%3Dhttp%3A%2F%2Fwww.wikihow.com%2Fmake-pizza-dough%26t%3D1396510456016%26n%3D11094%26k%3Dmainentity%3E+rdfs%3Alabel+%3Flabel+.+%0D%0A++%3Chttp%3A%2F%2Fvocab.inf.ed.ac.uk%2Fprocont%23%3Furl%3Dhttp%3A%2F%2Fwww.wikihow.com%2Fmake-pizza-dough%26t%3D1396510456016%26n%3D11094%26k%3Dmainentity%3E+rdf%3Atype+%2F+rdfs%3AsubClassOf%2A+%3Ftype%0D%0A%7D+LIMIT+100)
```
SELECT ?label ?type WHERE { 
  <http://vocab.inf.ed.ac.uk/procont#?url=http://www.wikihow.com/make-pizza-dough&t=1396510456016&n=11094&k=mainentity> rdfs:label ?label . 
  <http://vocab.inf.ed.ac.uk/procont#?url=http://www.wikihow.com/make-pizza-dough&t=1396510456016&n=11094&k=mainentity> rdf:type / rdfs:subClassOf* ?type
} LIMIT 100
```

Query 6) Select the various methods of a process (query result is empty if the process does not have sub-methods). [Try it!](https://w3id.org/knowhow/sparql?query=PREFIX+prohow%3A+%3Chttp%3A%2F%2Fw3id.org%2Fprohow%23%3E+%0D%0APREFIX+rdf%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F1999%2F02%2F22-rdf-syntax-ns%23%3E+%0D%0APREFIX+rdfs%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23%3E+%0D%0APREFIX+oa%3A+%3Chttp%3A%2F%2Fwww.w3.org%2Fns%2Foa%23%3E+%0D%0A%0D%0ASELECT+%3Fmethod+%3Flabel+WHERE+%7B+%0D%0A++%3Chttp%3A%2F%2Fvocab.inf.ed.ac.uk%2Fprocont%23%3Furl%3Dhttp%3A%2F%2Fwww.wikihow.com%2Fchange-the-timezone-in-linux%26t%3D1396533103326%26n%3D1098052%26k%3Dmainentity%3E+prohow%3Ahas_method+%3Fmethod+.+%0D%0A++%3Fmethod+rdfs%3Alabel+%3Flabel+%0D%0A%7D+LIMIT+100)
 ```
SELECT ?method ?label WHERE { 
  <http://vocab.inf.ed.ac.uk/procont#?url=http://www.wikihow.com/create-an-email-account&t=1396532526446&n=1068622&k=mainentity> prohow:has_method ?method . 
  ?method rdfs:label ?label 
} LIMIT 100
```
Query 7) Select the various steps of a process (query result is empty if the process does not have sub-steps). [Try it!](https://w3id.org/knowhow/sparql?query=PREFIX+prohow%3A+%3Chttp%3A%2F%2Fw3id.org%2Fprohow%23%3E+%0D%0APREFIX+rdf%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F1999%2F02%2F22-rdf-syntax-ns%23%3E+%0D%0APREFIX+rdfs%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23%3E+%0D%0APREFIX+oa%3A+%3Chttp%3A%2F%2Fwww.w3.org%2Fns%2Foa%23%3E+%0D%0A%0D%0ASELECT+%3Fstep+%3Flabel+WHERE+%7B+%0D%0A++%3Chttp%3A%2F%2Fvocab.inf.ed.ac.uk%2Fprocont%23%3Furl%3Dhttp%3A%2F%2Fwww.wikihow.com%2Fchange-the-timezone-in-linux%26t%3D1396533103326%26n%3D1098060%3E+prohow%3Ahas_step+%3Fstep+.+%0D%0A++%3Fstep+rdfs%3Alabel+%3Flabel+%0D%0A%7D+LIMIT+100)
```
SELECT ?step ?label WHERE { 
  <http://vocab.inf.ed.ac.uk/procont#?url=http://www.wikihow.com/create-an-email-account&t=1396532526447&n=1068628> prohow:has_step ?step . 
  ?step rdfs:label ?label 
} LIMIT 100
 ```
 Query 8) Select the various requirements of a process (query result is empty if the process does not have requirements). [Try it!](https://w3id.org/knowhow/sparql?query=PREFIX+prohow%3A+%3Chttp%3A%2F%2Fw3id.org%2Fprohow%23%3E+%0D%0APREFIX+rdf%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F1999%2F02%2F22-rdf-syntax-ns%23%3E+%0D%0APREFIX+rdfs%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23%3E+%0D%0APREFIX+oa%3A+%3Chttp%3A%2F%2Fwww.w3.org%2Fns%2Foa%23%3E+%0D%0A%0D%0ASELECT+%3Frequirement+%3Flabel+WHERE+%7B+%0D%0A++%3Chttp%3A%2F%2Fvocab.inf.ed.ac.uk%2Fprocont%23%3Furl%3Dhttp%3A%2F%2Fwww.wikihow.com%2Fmake-pizza-dough%26t%3D1396510456016%26n%3D11094%26k%3Dmainentity%3E+prohow%3Arequires+%3Frequirement+.+%0D%0A++%3Frequirement+rdfs%3Alabel+%3Flabel+%0D%0A%7D+LIMIT+100)
  ```
SELECT ?requirement ?label WHERE { 
  <http://vocab.inf.ed.ac.uk/procont#?url=http://www.wikihow.com/make-pizza-dough&t=1396510456016&n=11094&k=mainentity> prohow:requires ?requirement . 
  ?requirement rdfs:label ?label 
} LIMIT 100
 ```
 Query 9) Like Query 8), but optionally return the DBpedia resource linked to each requirement (when available). [Try it!](https://w3id.org/knowhow/sparql?query=PREFIX+prohow%3A+%3Chttp%3A%2F%2Fw3id.org%2Fprohow%23%3E+%0D%0APREFIX+rdf%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F1999%2F02%2F22-rdf-syntax-ns%23%3E+%0D%0APREFIX+rdfs%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23%3E+%0D%0APREFIX+oa%3A+%3Chttp%3A%2F%2Fwww.w3.org%2Fns%2Foa%23%3E+%0D%0A%0D%0ASELECT+%3Frequirement+%3Flabel+%3Ftype+WHERE+%7B+%0D%0A++%3Chttp%3A%2F%2Fvocab.inf.ed.ac.uk%2Fprocont%23%3Furl%3Dhttp%3A%2F%2Fwww.wikihow.com%2Fmake-pizza-dough%26t%3D1396510456016%26n%3D11094%26k%3Dmainentity%3E+prohow%3Arequires+%3Frequirement+.+%0D%0A++%3Frequirement+rdfs%3Alabel+%3Flabel+%0D%0A++OPTIONAL+%7B%3Frequirement+rdf%3Atype+%3Ftype%7D+%0D%0A%7D+LIMIT+100)
  ```
SELECT ?requirement ?label ?type WHERE { 
  <http://vocab.inf.ed.ac.uk/procont#?url=http://www.wikihow.com/make-pizza-dough&t=1396510456016&n=11094&k=mainentity> prohow:requires ?requirement . 
  ?requirement rdfs:label ?label 
  OPTIONAL {?requirement rdf:type ?type} 
} LIMIT 100
 ```
 Query 10) Find the 100 most common requirements. [Try it!](https://w3id.org/knowhow/sparql?query=PREFIX+prohow%3A+%3Chttp%3A%2F%2Fw3id.org%2Fprohow%23%3E+%0D%0APREFIX+rdf%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F1999%2F02%2F22-rdf-syntax-ns%23%3E+%0D%0APREFIX+rdfs%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23%3E+%0D%0APREFIX+oa%3A+%3Chttp%3A%2F%2Fwww.w3.org%2Fns%2Foa%23%3E+%0D%0A%0D%0ASELECT+%3Ftype+%28COUNT+%28DISTINCT+%3Fmain%29+as+%3Fno%29+WHERE+%7B+%0D%0A++%3Fmain+prohow%3Arequires+%3Frequirement+.%0D%0A++%3Frequirement+rdf%3Atype+%3Ftype%0D%0A%7D+GROUP+BY+%3Ftype+%3Fno+ORDER+BY+desc%28%3Fno%29+LIMIT+100)
  ```
SELECT ?type (COUNT (DISTINCT ?main) as ?no) WHERE { 
  ?main prohow:requires ?requirement .
  ?requirement rdf:type ?type
} GROUP BY ?type ?no ORDER BY desc(?no) LIMIT 100
 ```
  Query 11) Find the 100 most common outputs. [Try it!](https://w3id.org/knowhow/sparql?query=PREFIX+prohow%3A+%3Chttp%3A%2F%2Fw3id.org%2Fprohow%23%3E+%0D%0APREFIX+rdf%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F1999%2F02%2F22-rdf-syntax-ns%23%3E+%0D%0APREFIX+rdfs%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23%3E+%0D%0APREFIX+oa%3A+%3Chttp%3A%2F%2Fwww.w3.org%2Fns%2Foa%23%3E+%0D%0A%0D%0ASELECT+%3Ftype+%28COUNT+%28DISTINCT+%3Foutput%29+as+%3Fno%29+WHERE+%7B+%0D%0A++%3Fmain+rdf%3Atype+prohow%3Ainstruction_set+.%0D%0A++%3Foutput+prohow%3Ahas_method+%3Fmain+.%0D%0A++%3Foutput+rdf%3Atype+%3Ftype%0D%0A%7D+GROUP+BY+%3Ftype+%3Fno+ORDER+BY+desc%28%3Fno%29+LIMIT+100)
  ```
SELECT ?type (COUNT (DISTINCT ?output) as ?no) WHERE { 
  ?main rdf:type prohow:instruction_set .
  ?output prohow:has_method ?main .
  ?output rdf:type ?type
} GROUP BY ?type ?no ORDER BY desc(?no) LIMIT 100
 ```
 Query 12) Find the type of requirements most correlated with a particular requirement (in this example, the query can be interpreted as: "*what is usually used in conjunction with Paper*"?). [Try it!](https://w3id.org/knowhow/sparql?query=PREFIX%20prohow%3A%20%3Chttp%3A%2F%2Fw3id.org%2Fprohow%23%3E%20%0APREFIX%20rdf%3A%20%3Chttp%3A%2F%2Fwww.w3.org%2F1999%2F02%2F22-rdf-syntax-ns%23%3E%20%0APREFIX%20rdfs%3A%20%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23%3E%20%0APREFIX%20oa%3A%20%3Chttp%3A%2F%2Fwww.w3.org%2Fns%2Foa%23%3E%20%0A%0ASELECT%20%3Ftype%20(COUNT%20(DISTINCT%20%3Fother_req)%20as%20%3Fno)%0AWHERE%20%7B%20%0A%20%20%3Fmain%20rdf%3Atype%20prohow%3Ainstruction_set%20.%0A%20%20%3Fmain%20prohow%3Arequires%20%3Frequirement%20.%20%0A%20%20%3Frequirement%20rdf%3Atype%20%3Chttp%3A%2F%2Fdbpedia.org%2Fresource%2FPaper%3E%20.%0A%20%20%3Fmain%20prohow%3Arequires%20%3Fother_req%20.%20%0A%20%20%3Fother_req%20rdf%3Atype%20%3Ftype%0A%20%20FILTER%20(%3Ftype%20!%3D%20%3Chttp%3A%2F%2Fdbpedia.org%2Fresource%2FPaper%3E)%0A%7D%20GROUP%20BY%20%3Ftype%20ORDER%20BY%20desc(%3Fno)%20LIMIT%2020)
  ```
SELECT ?type (COUNT (DISTINCT ?other_req) as ?no)
WHERE { 
  ?main rdf:type prohow:instruction_set .
  ?main prohow:requires ?requirement . 
  ?requirement rdf:type <http://dbpedia.org/resource/Paper> .
  ?main prohow:requires ?other_req . 
  ?other_req rdf:type ?type
  FILTER (?type != <http://dbpedia.org/resource/Paper>)
} GROUP BY ?type ORDER BY desc(?no) LIMIT 20
 ```
 Query 13) The Linked Data representation of instructions is linked to the web documents it was extracted from using the [Open Annotation](http://www.openannotation.org/spec/core/) data model. This query finds the original source webpages of 20 instruction entities, along with the exact text span they relate to: [Try it!](https://w3id.org/knowhow/sparql?query=PREFIX%20prohow%3A%20%3Chttp%3A%2F%2Fw3id.org%2Fprohow%23%3E%20%0APREFIX%20rdf%3A%20%3Chttp%3A%2F%2Fwww.w3.org%2F1999%2F02%2F22-rdf-syntax-ns%23%3E%20%0APREFIX%20rdfs%3A%20%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23%3E%20%0APREFIX%20oa%3A%20%3Chttp%3A%2F%2Fwww.w3.org%2Fns%2Foa%23%3E%20%0A%0ASELECT%20DISTINCT%20%3Fexact%20%3Fsource%20%3Fmain%0AWHERE%20%7B%20%0A%20%20%3Fannotation%20oa%3AhasBody%20%3Fmain%20.%20%0A%20%20%3Fmain%20rdf%3Atype%20prohow%3Ainstruction_set%20.%0A%20%20%3Fannotation%20oa%3AhasTarget%20%3Ftarget%20.%20%0A%20%20%3Ftarget%20oa%3AhasSource%20%3Fsource%20.%0A%20%20%3Ftarget%20oa%3AhasSelector%20%3Fselector%20.%0A%20%20%3Fselector%20oa%3Aexact%20%3Fexact%20.%0A%7D%20LIMIT%2020)
  ```
SELECT DISTINCT ?exact ?source ?main
WHERE { 
  ?annotation oa:hasBody ?main . 
  ?main rdf:type prohow:instruction_set .
  ?annotation oa:hasTarget ?target . 
  ?target oa:hasSource ?source .
  ?target oa:hasSelector ?selector .
  ?selector oa:exact ?exact .
} LIMIT 20
  ```
  
Query 14) The [multilingual version of the dataset](https://www.kaggle.com/paolop/human-instructions-multilingual-wikihow) contains different versions in different languages of the same set of instructions. If you are using this data, you can use this query to find out pairs of instructions in different languages, along with their label, which refer to the same set of instructions: [Try it!](http://dydra.com/paolo-pareti/wikihow_multilingual/query?query=PREFIX%20prohow%3A%20%3Chttp%3A%2F%2Fw3id.org%2Fprohow%23%3E%20%0APREFIX%20rdf%3A%20%3Chttp%3A%2F%2Fwww.w3.org%2F1999%2F02%2F22-rdf-syntax-ns%23%3E%20%0APREFIX%20rdfs%3A%20%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23%3E%20%0APREFIX%20owl%3A%20%3Chttp%3A%2F%2Fwww.w3.org%2F2002%2F07%2Fowl%23%3E%20%0APREFIX%20oa%3A%20%3Chttp%3A%2F%2Fwww.w3.org%2Fns%2Foa%23%3E%20%0A%0ASELECT%20DISTINCT%20%3Fa%20%3Fb%20%3Fa_label%20%3Fb_label%0AWHERE%20%7B%0A%3Fa%20rdf%3Atype%20prohow%3Ainstruction_set%20.%0A%3Fb%20rdf%3Atype%20prohow%3Ainstruction_set%20.%0A%3Fann_a%20oa%3AhasBody%20%3Fa%20.%0A%3Fann_b%20oa%3AhasBody%20%3Fb%20.%0A%3Fann_a%20oa%3AhasTarget%20%3Ftar_a%20.%0A%3Fann_b%20oa%3AhasTarget%20%3Ftar_b%20.%0A%3Ftar_a%20owl%3AsameAs%20%3Ftar_b%20.%20%0A%3Fa%20rdfs%3Alabel%20%3Fa_label%20.%20%0A%3Fb%20rdfs%3Alabel%20%3Fb_label%20.%20%0A%7D)
  ```
SELECT DISTINCT ?a ?b ?a_label ?b_label
WHERE {
  ?a rdf:type prohow:instruction_set .
  ?b rdf:type prohow:instruction_set .
  ?ann_a oa:hasBody ?a .
  ?ann_b oa:hasBody ?b .
  ?ann_a oa:hasTarget ?tar_a .
  ?ann_b oa:hasTarget ?tar_b .
  ?tar_a owl:sameAs ?tar_b . 
  ?a rdfs:label ?a_label . 
  ?b rdfs:label ?b_label . 
}
  ```
