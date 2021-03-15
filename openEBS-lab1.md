
[OpenEBS Architeture](https://docs.openebs.io/docs/next/quickstart.html)


https://github.com/openebs/openebs/blob/master/contribute/design/README.md


Understand the pre-requisites for your Kubernetes platform
Start installation through OpenEBS operator.
For production deployments or to test OpenEBS volumes on real disks, create cStorPools, cStor-StorageClasses and start provisioning volumes using the newly created cStor-StorageClasses. More details can be found from here.
For applications requiring high performance, which manage their own replication, data protection and other storage features, provision OpenEBS Local PV. More details can be found here.


为何选择openebs? 

https://zhuanlan.zhihu.com/p/342387421

Portworx和OpenEBS是AKS最快的容器存储。
围绕NVMe的稳健设计，OpenEBS似乎已成为最好的开源容器存储选项之一。
对于简单的块存储用例，Longhorn绝对是有效的选择，它与OpenEBS Jiva后端非常相似。
https://zhuanlan.zhihu.com/p/337076325

OpenEBS需要使用iSCSI作为存储协议
 


