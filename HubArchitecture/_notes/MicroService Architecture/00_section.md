# Demo
For this demo, Instead of using hub as our demo project in this showcase, I'm going to use a small but complete custom project as demo project, because Hub just started, there is no enough data and functionality to illustrate the whole infrastructor.

But no matter which project we are using, they are exactly the same.

So Let's take a quick preview of our demo application.

# The architecture of Microservice
In order to have a more better understanding of our Docker Infrastructure, so firstly, I will gave you a brief description of this demo application. The demo application is a typical micro-service application.

This project is a typcal microservice architecture. It was decomposed into three core microservices. All of them are independently deployable applications, organized around certain business domains.

- Account service
- Statistics service
- Notification service

这是一个典型的微服务架构, 它包含3个模块, 并且每个模块都有自己对应的独立数据库, 3个模块之间使用 REST API 来进行通信.
为这种结构的微服务搭建服务器, 我们可能首先想到的就是设置6台主机, 分别运行这3个模块和他们对应的数据库.

但是今天我们要讲的是如何使用 docker 来搭建这种微服务架构的, 以及使用 docker 的优势.

# Infrastructure services
我们首先搭建了5台 docker 服务器, 并将这5台服务器通过 Local Area Network(LAN) 的方式连接到一起, 使他们成为一个cluster, 并且这里设置了两台服务器作为集群的 manager 服务器, 来管理整个集群, 之所以设置2个服务器就是为了防止一种一台manager服务区宕掉后, 我们还有一台备用的manager服务器来管理整个集群.

所有的 docker 容器均匀的分布在这5台服务器中运行.

http://devdocker01.rtp.raleigh.ibm.com:8080/

We have totaly five servers, and these servers work together as one cluster.

The significant difference between a cluster and a group of servers is that the cluster acts as a single system trying to provide high availability, load balancing, and parallel processing.


- docker builder server: Used for manager
- docker01
- docker02
- docker03
- docker04