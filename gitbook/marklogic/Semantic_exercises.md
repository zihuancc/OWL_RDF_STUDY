## Semantic exercises
- data: 2017-8-17
- source: http://developer.marklogic.com/learn/semantics-exercises
- host:kunlun09.bbdops.com
#####后台 mlcp 工具导入数据
 > ./mlcp.sh import -host localhost -port 8000 -username admin -password bbd123 -input_file_path /data1/kunlun-volumes/markLogic/opt/data_test/semantics-exercises/data/dbpedia60k.nt  -mode local -output_uri_prefix /person/ --input_file_type rdf

#### Query Console
##### query
 prefix onto:<http://dbpedia.org/ontology/>   
 prefix sr:<http://dbpedia.org/resource/>  
 SELECT ?s ?p ?o  
 WHERE { ?s onto:birthPlace sr:Brooklyn;  
       ?p ?o}   

