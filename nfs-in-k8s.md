# nfs in k8s 

## pv with nfs 

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: nfs-pv
spec:
  capacity:
    storage: 5Gi
  volumeMode: Filesystem
  accessModes:
  - ReadWriteOnce
  persistentVolumeReclaimPolicy: Recycle
  storageClassName: slow
  mountOptions:
  - hard
  - nfsvers=4.1
  nfs:
    path: /tmp
    server: 192.168.5.150

---
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: pvc001
  namespace: default
spec:
  accessModes:
  - ReadWriteMany
  resources:
    requests:
      storage: 1Gi
---
apiVersion: v1
kind: Pod
metadata:
  name: pod-use-pvc
  namespace: default
spec:
  containers:
  - name: busybox
    image: busybox:1.28
    command: ["sleep","3600"]
    volumeMounts:
    - name: code
      mountPath: /data/
  volumes:
  - name: code
    persistentVolumeClaim:
      claimName: pvc001
```

## pod with nfs volume 

```yaml
apiVersion: apps/v1 
kind: Deployment
metadata:
  name: redis
spec:
  selector:
    matchLabels:
      app: redis
  revisionHistoryLimit: 2
  template:
    metadata:
      labels:
        app: redis
    spec:
      containers:
      - image: redis
        name: redis
        imagePullPolicy: IfNotPresent
        ports:
        - containerPort: 6379
          name: redis6379
        env:
        - name: ALLOW_EMPTY_PASSWORD
          value: "yes"
        - name: REDIS_PASSWORD
          value: "redis"          
# 持久化挂接位置，在docker中 
        volumeMounts:
        - name: redis-persistent-storage
          mountPath: /data
      volumes:      
# 宿主机上的目录
      - name: redis-persistent-storage
        nfs:
          path: /k8s-nfs/redis/data
          server: 192.168.8.150
```

## nfs provisioner

[root@node01 src]# cat deployment.yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nfs-client-provisioner
  labels:
    app: nfs-client-provisioner
  # replace with namespace where provisioner is deployed
  namespace: default
spec:
  replicas: 1
  strategy:
    type: Recreate
  selector:
    matchLabels:
      app: nfs-client-provisioner
  template:
    metadata:
      labels:
        app: nfs-client-provisioner
    spec:
      serviceAccountName: nfs-client-provisioner
      containers:
        - name: nfs-client-provisioner
          image: pastack-registry.paic.com.cn/pac-yunguan/nfs-client-provisioner:3.1.0
          imagePullPolicy: IfNotPresent
          volumeMounts:
            - name: nfs-client-root
              mountPath: /persistentvolumes
          env:
            - name: PROVISIONER_NAME
              value: nfs.provisioner1
            - name: NFS_SERVER
              value: 30.103.2.9
            - name: NFS_PATH
              value: /data/k8snfs
      volumes:
        - name: nfs-client-root
          nfs:
            server: 30.103.2.9
            path: /data/k8snfs
[root@node01 src]# cat storageclass.yml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: managed-nfs-storage
reclaimPolicy: Retain
allowVolumeExpansion: true
provisioner: nfs.provisioner1
parameters:
  archiveOnDelete: "false"
[root@node01 src]#

