# 4.2.6
## ReplicaController水平缩放pod
```
$ k scale rc kubia --replicas=10
```

## 通过编辑器，修改spec.replicas字段
```
$ k edit rc kubia
```

# 4.3.5
## 删除ReplicaSet可以删除集群
```
$ k delete rs kubia
```

## ReplicaSet水平缩放pod
```
$ k scale rs kubiars --replicas=10
```

## 通过编辑器，修改spec.replicas字段
```
$ k edit rs kubiars
```