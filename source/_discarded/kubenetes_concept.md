title: kubernetes从入门到放弃--k8s基本概念
catalog: true
toc_nav_num: true
subtitle: kubernetes基本概念
header-img: 'http://cdn.hanyajun.com/article_header.png'
tags:
  - kubernetes
  - ''
categories:
  - kubernetes
  - ''
author: 韩亚军
date: 2019-04-18 10:51:00
---
#### kubernetes架构图

下图为kubernetes的master架构图
![image](https://jimmysong.io/kubernetes-handbook/images/kubernetes-high-level-component-archtecture.jpg)
### 1. **Cluster**   
cluster是计算、存储和网络资源的集合，kubernetes利用这些资源运行各种基于容器的应用。
### 2. **Master**  
Master 是Cluster的大脑，它的主要职能就是负责调度，决定应用放在哪里运行。master运行linux操作系统，可以是物理机或者虚拟机。为了实现高可用，可以运行多个Master。
### 3. Node
Node 的职责是运行容器应用。Node由Master管理，Node负责监控并汇报容器的状态，同时根据Master的要求管理容器的生命周期。Node运行在linux系统上，可以是物理机或者虚拟机。
### 4. Pod
Pod是kubernetes的最小工作单元。每个pod可以包含一个或者多个容器。Pod中的容器会作为一个整体被Master调度到一个Node上运行。kubernetes 以**Pod**为最小单位进行调度、扩展、共享资源、管理生命周期；pod中的所有容器都共享一个网络namespace，所有的容器可以共享存储。
- pod有两种使用方式：
1. 运行单一容器：<br>
   one-container-per-Pod 是kubernetes最常见的模型，这种情况下，只是将单个容器简单封装成pod。即使只有一个容器，kubernetes管理的也是pod而不是直接管理容器。
2. 运行多个容器:<br>
   运行在同一个pod的的多个容器必须联系紧密，而且直接共享资源。

### 5. Controller
 kubernetes通常不会直接去创建pod，而是通过Controller去管理pod的，Controller中定义了Pod的部署特性，比如有几个副本、什么样的Node上运行等。为了满足不同的业务场景，kubernetes提供了多种Controller，包括Deployment、ReplicaSet、DeamonSet、StatefuleSet、Job等，我们逐一讨论。

- Deployment :是最常用的的Controller，deployment可以管理pod的多个副本，并确保pod按照预期的状态来运行。
- ReplicaSet : 实现了pod的多副本管理。使用Deployment时会自动创建Replicaset。
- DeamonSet: 用于每个Node最多只能运行一个Pod副本的场景。
- StatefuleSet:能够保证Pod的每个副本在整个生命周期中名称是不变的，而其它Controller是提供这个功能。当某个Pod发生故障需要删除并且重新启动时，Pod的名称会发生变化，同时StatefuleSet会保证副本按照固定的顺序启动、更新或者删除。
- Job 用于运行就删除的应用，而其他Controller　中的ｐｏｄ通常是持续运行的。

### 6. Service
Deployment 可以部署多个副本，每个Pod都有自己的Ip，那么外界如何访问这些副本呢？Kubernetes Service 定义了外界访问一组特定Pod的方式。Service 有自己的IP和端口，Service为pod提供了负载均衡。K8s运行容器Pod与访问容器Pod这两项任务分别由Controller和Service执行。
### 7. Namespace
 如果有多个用户或者项目组共同使用k8s 集群，如果将他们创建的Pod等资源分开呢，就是通过Namespace进行隔离。
