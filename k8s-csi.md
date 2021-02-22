# k8s CSI 

在 Kubernetes 容器平台中，Kubernetes 可以调用某类存储插件，对接后端存储服务，如调用 GCE 存储插件对接后端 GCE 存储服务。Kubernetes 里的存储插件可以分为 In-tree 和 Out-of-tree 这两大类。

Out-of-tree 存储插件现在分为 FlexVolume 和 CSI 两大类。FlexVolume 插件是 Kubernetes1.2 开始支持的，

另一种比较新的存储方案是 CSI 方案，CSI 方案全称是 Container Storage Interface，它是容器平台里的一种工业标准。CSI 不仅仅是针对 Kubernetes 容器平台开发的，它是一种容器平台的通用解决方案。存储服务商或者存储厂商只要开发支持 CSI 标准的存储插件，就可以供各种容器平台使用。Kubernetes 从 1.9 开始支持 CSI 规范。

[csi spec](https://github.com/container-storage-interface/spec/blob/master/spec.md)

[技术分享 | 基于 CSI Kubernetes 存储插件的开发实践](https://zhuanlan.zhihu.com/p/51757577)

https://feisky.gitbooks.io/kubernetes/content/plugins/csi.html



[深挖 Kubernetes 存储为何如此难及其解决方案](https://www.infoq.cn/article/mktBbeVcMILCAOXROgJ1)

https://cloud.tencent.com/developer/news/731936

## csi 使用方法

https://feisky.gitbooks.io/kubernetes/content/plugins/csi.html

https://kubernetes-csi.github.io/docs/drivers.html





## Ceph , Rook 

Rook 是一种云原生编排器，并对 Kubernetes 做出扩展。Rook 允许用户将 Ceph 放置在容器内，同时提供卷管理逻辑以立足 Kubernetes 之上实现 Ceph 的可靠运行。Rook 还使本应由集群管理员操作的多种任务完成了自动化实现，其中包括部署、引导、配置、扩展以及负载均衡等等。
Rook 可以像 Kubernetes 一样使用 yaml 文件来部署 Ceph 集群。这种文件以高级声明的形式存在，负责为集群管理员提供所需要的全部内容。
Rook 在集群启动完成后，即开始进行实时监控。Rook 将以操作端或者控制端的姿态确保 yaml 文件中所声明的状态始终正常。Rook 运行在一套协调的逻辑循环中，该循环将观察运行状态并根据检测到的异常采取响应。


深挖Kubernetes存储为何如此难及其解决方案
原文链接： https://www.infoq.cn/article/mktBbeVcMILCAOXROgJ1

## Longhorn

Longhorn 充分利用了近年来关于 如何编排大量的容器和虚拟机的核心技术 。例如，Longhorn 并没有构建一个可以扩展到 100,000 个 volume 的高度复杂的控制器，而是出于让存储控制器简单轻便的考虑，创建了 100,000 个单独的控制器。然后，我们可以利用像 Kubernetes 这样的最先进的编排系统来调度这些独立的控制器，共享一组磁盘中的资源，协同工作，形成一个弹性的分布式块存储系统。


Longhorn 基于微服务的设计还有很多其他优势。因为每个 volume 都有自己的控制器，在升级每个 volume 的控制器和 replica 容器时，是不会导致 IO 操作明显的中断的。

Longhorn 可以创建一个长期运行的工作来编排所有 live volume 的升级，同时确保不会中断系统正在进行的操作。为确保升级不会导致意外的问题，Longhorn 可以选择升级一小部分 volume，并在升级过程中出现问题时回滚到旧版本。这些做法在现代微服务应用中已得到广泛应用，但在存储系统中并不常见。希望 Longhorn 可以 助力于微服务在存储领域的更多应用。


深挖Kubernetes存储为何如此难及其解决方案
原文链接： https://www.infoq.cn/article/mktBbeVcMILCAOXROgJ1

### 入门教程

https://www.cnblogs.com/rancherlabs/p/12190718.html

待做实验

### 节点维护功能升级

Longhorn 1.1的另一个全新功能是增强的节点维护能力。Longhorn现已支持Kubernetes drain operations,以帮助用户安全地执行节点维护。Longhorn 1.1还具有识别新节点上现有磁盘的功能,从而为云供应商提供更好的操作环境。


## Rancher 2

[Rancher Get Started](https://docs.rancher.cn/docs/rancher2/quick-start-guide/deployment/quickstart-manual-setup/_index)

## Rancher应用商店

Longhorn是RancherLab为K8S环境研发的一种分布式块存储系统。Longhorn轻便易用，你可以用Kubectl命令，在一个现有的K8S集群上快速部署。结合Rancher2.0环境中的应用商店，还可以实现一键部署，为K8S集群环境提供动态的StorageClass持久卷支持。


## 看电影

http://www.diezhan.me/dalu/shanhaiqingyuanshengban/play-0-9.html

