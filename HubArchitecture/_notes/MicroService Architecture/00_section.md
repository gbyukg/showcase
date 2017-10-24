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
我们首先搭建了5台 docker 服务器, 并将这5台服务器通过 Local Area Network(LAN) 的方式连接到一起, 使他们成为一个集群, 设置为集群有两个最重要的好处
- 灵活性, 我们可以在任意时候随意向这个集群中增加或减少服务器
- 我们可以将这5台server当做一个整体来看待, 在部署某个docker容器的时候, 能让我们自动分配系统资源.

并且这里设置了两台服务器作为集群的 manager 服务器, 来管理整个集群, 之所以设置2个服务器就是为了防止一种一台manager服务区宕掉后, 我们还有一台备用的manager服务器来管理整个集群.

所有的 docker 容器均匀的分布在这5台服务器中运行.

http://devdocker01.rtp.raleigh.ibm.com:8080/

We have totaly five servers, and these servers work together as one cluster.

The significant difference between a cluster and a group of servers is that the cluster acts as a single system trying to provide high availability, load balancing, and parallel processing.

While, in the morning, some service might require a lot of memory, during the afternoon that usage might be lower.

# Capability

- Scaling up/down at any time (on need basis)
可以让我们在任何时刻随意修改运行的容器个数, 甚至来说, 可能上午的时候某个模块访问流量比较大, 我们就可以增加这个模块的运行数量来减少压力, 等到晚上的时候访问量可能恢复到正常, 这个时候我们就可以在把容器数恢复回来.

- Failure handling 容错率
容错率包括两种情况:
1. 某个容器down掉时, 会自动启动一个新的容器
2. 某个服务器整个down掉后, 会自动在其他服务器上运行这台服务器上运行的容器