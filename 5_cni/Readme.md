# 12.5 Сетевые решения CNI

* Запустил установку через kubespray
```bash
alex@upc:~/devops-projects/kuber $ sudo ansible-playbook -vvv -i inventory/local/hosts.ini cluster.yml

```

* В итоге скрипт отработал (фрагмент)
```bash
PLAY RECAP *************************************************************************************************************************************
localhost                  : ok=4    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
node1                      : ok=582  changed=107  unreachable=0    failed=0    skipped=1151 rescued=0    ignored=2   

Sunday 29 August 2021  19:43:09 +0700 (0:00:00.060)       0:10:08.743 ********* 

```

* Создал политику
```bash
alex@upc:~/devops-projects/kuber $ sudo kubectl create ns policy-my
namespace/policy-my created
```

* Задеплоил приложение в указанный неймспейс
```bash
alex@node1:~/devops-projects/kuber $ sudo kubectl apply --namespace=policy-my -f ./ctrl/nginx_hello.yaml 
deployment.apps/hello-node-srv configured

```

* приложение отображается в списке подов
```bash
alex@node1:~/devops-projects/kuber $ sudo kubectl get pods --all-namespaces
NAMESPACE     NAME                                       READY   STATUS    RESTARTS   AGE
kube-system   calico-kube-controllers-8575b76f66-jzht4   1/1     Running   2          100m
kube-system   calico-node-d8zb7                          1/1     Running   2          100m
kube-system   coredns-8474476ff8-lzcxh                   0/1     Running   1          100m
kube-system   dns-autoscaler-7df78bfcfb-vw9vn            1/1     Running   1          100m
kube-system   kube-apiserver-node1                       1/1     Running   1          102m
kube-system   kube-controller-manager-node1              1/1     Running   2          102m
kube-system   kube-proxy-xm4l7                           1/1     Running   0          23m
kube-system   kube-scheduler-node1                       1/1     Running   2          102m
kube-system   nodelocaldns-hpctv                         1/1     Running   1          100m
policy-my     hello-node-srv-75cbdb4d6-52spr             1/1     Running   0          11m
```

