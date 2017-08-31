## Cluster 
- 2017-08-24
- http://docs.marklogic.com/guide/cluster

#### Questions:
- Cluster Setup
- 数据是否自动分布存储,分布是否均匀
- 如何区别搭建 E-node & D-node
- E-node VS D-node , 实际作用测试

### Cluster Setup
#### Setup : Building a Cluster from Scratch
There are four key stages to build a cluster from scratch:

- Installing the initial host in the cluster
- Configuring the initial host with the groups and databases that you will be using in the cluster
- Filling out the cluster by installing the additional hosts and adding them to the cluster
- Configuring the forest layout within the cluster.

##### Section One : join a cluster
- 1. 单机安装方式安装、启动
- 2. 加入另外一个host，安装方式同上，启动后，'join a cluster'
>configuring: http://docs.marklogic.com/guide/installation/procedures#id_60220  

##### Section Two : create forests and databases
- 1. 创建forests
    - forest UNQ
    - 可以选择某个forest在哪台机器上
- 2. 创建database
    - databaes UNQ
    - 选择将哪些forests attached 到database上

##### Now, cluster is ready to use.

##### Section Three : Configurations
TODO
##### Section Four : HA
TODO
##### Section Five : Failover
TODO
### TESTING
```
```
