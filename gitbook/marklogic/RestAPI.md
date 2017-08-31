## REST API
- date: 2017-08-30
- https://docs.marklogic.com/guide/rest-dev/intro#id_16025

##### some examples
document 增加一个文件
```
 curl --anyauth --user admin:bbd123 -X PUT -d@'./one.xml' \
     -H "Content-type: application/xml" \
         'http://kunlun08.bbdops.com:8000/LATEST/test?uri=/xml/one.xml'
```

查询test所有
```
 curl --anyauth --user admin:bbd123 -i -X GET \
     -H "Accept: application/xml" \
     http://kunlun08.bbdops.com:8000/LATEST/search?database=test
```


