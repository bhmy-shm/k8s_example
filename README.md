# k8s_example
所有k8s组件Yaml手抄版，以及自用的yaml 模板

### Role | ClusterRole

查看 k8s资源：`kubectl api-resoucres -o wide`

#### 一、创建用户并赋予config上下文

[context-name] : 自定义的用户上下文名称

1.把用户设置写入到 kube/config 里面生效 证书 和 用户名
```shell script
kubectl config --kubeconfig=/root/.kube/config  \
set-credentials [user-name]  \
--client-certificate=/root/k8s/ssl/client.crt \
--client-key=/root/k8s/ssl/client.key
```

2.设置用户能够使用的context上下文
```shell script
kubectl config --kubeconfig=/root/.kube/config \
set-context [context-name] --cluster=kubernetes  --user=[user-name]
```

3.指定切换context上下文
```shell script
kubectl config --kubeconfig=/root/.kube/config \
use-context [context-name]
```

4.切换回管理员

kubernetes-admin@kubernetes 默认管理员上下文
```shell script
kubectl config use-context kubernetes-admin@kubernetes
```

#### 二、Role角色命令行绑定
格式如下：

- binding-name：自定义rolebinding名称
- role-name: 自定义角色名称
- user-name: 认证的上下文中的用户

```shell script
kubectl create rolebinding [binding-name] \
-n [namespaces] \
--role=[role-name] \
--user [user-name]
```

#### 三、Cluster角色命令行绑定
格式如下：
- 
```shell script
kubectl create clusterRobinding [binding-name] \
-n [namespaces] \
--clusterrole=[role-name] \
--user [user-name]
```