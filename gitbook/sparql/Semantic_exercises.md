## Semantic exercises
- data: 2017-8-17
- source: http://developer.marklogic.com/learn/semantics-exercises
- host:kunlun09.bbdops.com
#####后台 mlcp 工具导入数据
 > ./mlcp.sh import -host localhost -port 8000 -username admin -password bbd123 -input_file_path /data1/kunlun-volumes/markLogic/opt/data_test/semantics-exercises/data/dbpedia60k.nt  -mode local -output_uri_prefix /person/ --input_file_type rdf

#### Query Console


##### insert data
```
prefix xsd:  <http://www.w3.org/2001/XMLSchema#> 
INSERT DATA
{
      GRAPH <TEST> {<book2> <title> "book2" }
        GRAPH <TEST> {<book3> <title> "book3" } 
          GRAPH <TEST> {<book4> <title> "book4" }
            GRAPH <TEST> {<book5> <title> "book5" }   
              GRAPH <TEST> {<book5> <publish_date> "2017-08" }
                GRAPH <TEST> {<book2> <publish_date> "2017-08" }
                  GRAPH <TEST> {<book2> <child> <book4> }   
                    GRAPH <TEST> {<book2> <number> "100"^^xsd:integer }
                      GRAPH <TEST> {<book4> <child> <book6> }
                        GRAPH <TEST> {<book6> <title> "book6"@cn }
                          GRAPH <TEST> {<book6> <title> "book6"@en }
                            GRAPH <TEST> {<book6> <title> "book6" }
                              
}
```
##### clear
```
CLEAR GRAPH <<TEST>>
```
##### delete
```
delete data
{
    GRAPH <<BOOKS1>>
        {
                <<http://example/book1> <http://purl.org/dc/elements/1.1/title>> "A new book"
        }
}
```
##### drop
```
drop GRAPH  <<http://marklogic.com/semantics/animals/vertebrates>>
```
#### 
##### query
1.查找负荷某些属性的triples
```
 prefix onto:<<http://dbpedia.org/ontology/>>   
 prefix sr:<<http://dbpedia.org/resource/>>  
 SELECT ?s ?p ?o  
 WHERE { ?s onto:birthPlace sr:Brooklyn;  
       ?p ?o}   
```
2.简化查找符合某些属性的数据triples
```
select ?o ?p ?s
where{
      ?o  <title> "book2";
        ?p ?s
}
```
3.查找属性为title的triples
```
select ?o  ?s
where{
      ?o  <title> ?s
}
```
4.多值匹配
all the variables used in the query pattern must be bound in every solution
每个变量都必须满足才会有返回值.
```
select ?o  ?title ?child
where{
    GRAPH <TEST>{
        ?o  <title> ?title .
        ?o  <child> ?child
    }
}
```
```

select ?o  ?title  ?number
where{
      GRAPH <TEST>{
            ?o  <title> ?title .
            ?o  <number> ?number 
      }
}
```
> 
[{"o":"<book2>","title":"\"book2\"","number":"\"100\"^^xs:integer"},{"o":"<book4>","title":"\"book4\"","number":"\"99\"^^xs:integer"}]

5.language tag
```
GRAPH <TEST> {<book6> <title> "book6"@cn }   
GRAPH <TEST> {<book6> <title> "book6"@en }  
GRAPH <TEST> {<book6> <title> "book6" }  
 有不一样的数据,值返回完全符合检索条件的
```
```
select ?o ?p 
where{
    GRAPH <TEST>{
    ?o  ?p "book6"@cn
    }
}
```
- 只返回一条数据
6.numeric type
```
select ?o ?p 
where{
    GRAPH <TEST>{
        ?o  ?p 100
    }
}
```
> [{"o":"<book2>","p":"<number>"}]
返回值不用加type限定词

7.Expressions
```
select (concat(?o , "  ", ?p ) as ?name)
where{
      GRAPH <TEST>{
                  ?o  ?p 100
                        }
}
- 返回组合的结果
```
或者
```
select ?name
where{
    GRAPH <TEST>{
        ?o  ?p 100
        bind(concat(?o , "  ", ?p ) as ?name)
    }
}
```
8.building rdf graph
```
construct {?o ?p ?s}
where{
      GRAPH <TEST>{
                  ?o  <number> 100;
                          ?s ?p
                                }
}
```
result
> {"book2":{"100":[{"value":"number","type":"uri"}],"book4":[{"value":"child","type":"uri"}],"book2":[{"value":"title","type":"uri"}],"2017-08":[{"value":"publish_date","type":"uri"}]}}

9.values: providing inline data 

```
select ?o ?p ?s ?k
where
{
      values ?o {<book2> <book4>}
               ?o <title> ?s;
                           <number> ?k
}
```

---
