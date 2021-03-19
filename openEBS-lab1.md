
[OpenEBS Architeture](https://docs.openebs.io/docs/next/quickstart.html)


https://github.com/openebs/openebs/blob/master/contribute/design/README.md


Understand the pre-requisites for your Kubernetes platform
Start installation through OpenEBS operator.
For production deployments or to test OpenEBS volumes on real disks, create cStorPools, cStor-StorageClasses and start provisioning volumes using the newly created cStor-StorageClasses. More details can be found from here.
For applications requiring high performance, which manage their own replication, data protection and other storage features, provision OpenEBS Local PV. More details can be found here.

使用容器化块存储OpenEBS在K3s中实现持久化存储
https://blog.csdn.net/qq_42206813/article/details/106358156

[CAS存储现状](https://cloud.tencent.com/developer/article/1548227)


https://blog.csdn.net/rancherlabs/article/details/71080450



## openEBS 

https://jishuin.proginn.com/p/763bfbd36b92

jiva其实就是longHorn 

开源存储特性对比
https://kubevious.io/blog/post/comparing-top-storage-solutions-for-kubernetes

https://openebs.io/blog/mayastor-nvme-of-tcp-performance/

https://www.percona.com/blog/2020/11/12/measuring-openebs-local-volume-performance-overhead-in-kubernetes/

性能对比：http://blog.itpub.net/69950566/viewspace-2668154/
　

[pvc mount as block device testcase](https://cloud.yandex.com/docs/managed-kubernetes/operations/volumes/mode-block)

apiVersion: v1
kind: Pod
metadata:
  name: pod
spec:
  containers:
  - name: app
    image: ubuntu
    command: ["/bin/sh"]
    args: ["-xc", "/bin/dd if=/dev/block of=/dev/null bs=1K count=10; /bin/sleep 3600"]
    volumeDevices:
    - devicePath: /dev/block
      name: persistent-storage
  volumes:
  - name: persistent-storage
    persistentVolumeClaim:
      claimName:  pvc-block


[volume expand testcase](https://cloud.yandex.com/docs/managed-kubernetes/operations/volumes/volume-expansion)
