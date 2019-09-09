# linux
## 设置主机名称
nmtui
## 安装docker-compose
- 安装pip
```
yum -y install epel-release
yum -y install python-pip
```
- 更新pip
```
pip install --upgrade pip
```
- 安装docker-compose
```
pip install docker-compose
```
## k8s 

### 遇到节点为ScheduleDisabled情况
```
[root@master ~]# kubectl get nodes
NAME     STATUS                     ROLES    AGE    VERSION
master   Ready                      master   356d   v1.10.5
tnode1   Ready                      master   356d   v1.10.5
tnode2   Ready                      master   356d   v1.10.5
tnode3   Ready,SchedulingDisabled   <none>   356d   v1.10.5
tnode4   Ready                      <none>   356d   v1.10.5
tnode5   Ready                      <none>   356d   v1.10.5
tnode6   Ready                      <none>   248d   v1.10.5
[root@master ~]# kubectl patch node tnode3 -p '{"spec":{"unschedulable":false}}'
node/tnode3 patched
[root@master ~]# kubectl get nodes
NAME     STATUS   ROLES    AGE    VERSION
master   Ready    master   356d   v1.10.5
tnode1   Ready    master   356d   v1.10.5
tnode2   Ready    master   356d   v1.10.5
tnode3   Ready    <none>   356d   v1.10.5
tnode4   Ready    <none>   356d   v1.10.5
tnode5   Ready    <none>   356d   v1.10.5
tnode6   Ready    <none>   248d   v1.10.5
[root@master ~]# kubectl patch node tnode3 -p '{"spec":{"unschedulable":true}}'
[root@master ~]# kubectl get nodes
NAME     STATUS                     ROLES    AGE    VERSION
master   Ready                      master   356d   v1.10.5
tnode1   Ready                      master   356d   v1.10.5
tnode2   Ready                      master   356d   v1.10.5
tnode3   Ready,SchedulingDisabled   <none>   356d   v1.10.5
tnode4   Ready                      <none>   356d   v1.10.5
tnode5   Ready                      <none>   356d   v1.10.5
tnode6   Ready                      <none>   248d   v1.10.5

```

### 时间同步
```
ntpdate time.nist.gov
```
