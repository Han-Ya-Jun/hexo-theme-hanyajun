title: kubernetes从入门到放弃--k8s基本架构
catalog: true
toc_nav_num: true
subtitle: kubernetes基本架构
header-img: 'http://cdn.hanyajun.com/article_header.png'
author: 韩亚军
top: 9
tags:
  - kubernetes
categories:
  - kubernetes
  - ''
date: 2019-04-20 23:15:00
---
### kubernetes总架构图 
![image](http://cdn.hanyajun.com/k8s-arch.jpg)
### kubernetes 各组件介绍
#### Master 节点
Master是kubernetes的大脑，运行的Deamon 服务包括kube-apiserver、kube-scheduler、kube-contronller-

manager、etcd和pod网络

![image](http://cdn.hanyajun.com/k8s_master.jpeg)
##### 各组件介绍
- **API Server**（kube-apiserver）</br> 

  API Server提供HTTP/HTTPS RESTful API，即Kubernetes API。API Server是Kubernetes　Cluster的前端接

  口，各种客户端工具（CLI或UI）以及Kubernetes其他组件可以通过它管理Cluster的各种资源。
- **Scheduler**（kube-scheduler） </br> 
  
  Scheduler负责决定将Pod放在哪个Node上运行。Scheduler在调度时会充分考虑Cluster的拓扑结构，当前各个

  节点的负载，以及应用对高可用、性能、数据亲和性的需求。
- **Controller Manager**（kube-controller-manager） </br> 

  Controller Manager负责管理Cluster各种资源，保证资源处于预期的状态。Controller Manager由多种Controller
  
  组成，包括replication controller、endpoint controller、namespace controller、serviceaccounts controller等。 
  
  不同的controller管理不同的资源。例如，replication controller管理Deployment、StatefulSet、DaemonSet的生
  
  命周期，namespace controller管理Namespace资源。
- **etcd** </br> 

  etcd负责保存Kubernetes Cluster的配置信息和各种资源的状态信息。当数据发生变化时，etcd会快速通知
  
  Kubernetes相关组件。
- **Pod网络** </br> 

  Pod要能够相同通信，Kubernetes Cluster必须部署Pod网络，flannel是其中一个可选方案。

##### master工作流程图
![image](http://cdn.hanyajun.com/k8s_master_workflow.png)
1. Kubecfg将特定的请求，比如创建Pod，发送给Kubernetes Client。

1. Kubernetes Client将请求发送给API server。

1. API Server根据请求的类型，比如创建Pod时storage类型是pods，然后依此选择何种REST Storage API对请求作出处理。

1. REST Storage API对的请求作相应的处理。
1. 将处理的结果存入高可用键值存储系统Etcd中。
1. 在API Server响应Kubecfg的请求后，Scheduler会根据Kubernetes Client获取集群中运行Pod及Minion/Node信息。
1. 依据从Kubernetes Client获取的信息，Scheduler将未分发的Pod分发到可用的Minion/Node节点上。

#### Node节点
Node节点属于工作节点,是pod运行的地方。

![image](http://cdn.hanyajun.com/k8s_node.jpg)

##### 各组件介绍
1. **kubelet**　<br>

   node的agent，当scheduler去确定在某个node上运行pod后，会将pod的具体配置信息发送给该节点的
   
   kubelet， kubelet会根据遮羞信息创建和运行容器，并向master报告运行状态。

2. **kube-proxy** <br>

    每个node都会运行kube-proxy服务，外界通过service访问pod，kube-proxy负责将降访问service的TCP/UDP数
    
    据流转发到后端的容器。如果有多个副本，kube-proxy会实现负载均衡。

 3. **pod网络**  <br>

    pod能能够互相通信，k8s集群必须部署pod网络，flannel是其中一个可以选择的方案
##### kubectl 架构解读
![image](http://cdn.hanyajun.com/kubelet.png)

###### Kubelet[节点上的Pod管家]
负责Node节点上pod的创建、修改、监控、删除等全生命周期的管理
定时上报本Node的状态信息给API Server。

kubelet是Master API Server和Minion/Node之间的桥梁，接收Master API Server分配给它的commands和work，

通过kube-apiserver间接与Etcd集群交互，读取配置信息。
具体的工作如下：
1. 设置容器的环境变量、给容器绑定Volume、给容器绑定Port、根据指定的Pod运行一个单一容器、给指定的Pod创建network 容器。

1. 同步Pod的状态、同步Pod的状态、从cAdvisor获取container info、 pod info、 root info、 machine info。
1. 在容器中运行命令、杀死容器、删除Pod的所有容器。

参考链接：https://yq.aliyun.com/articles/47308?spm=5176.100240.searchblog.19.jF7FFa