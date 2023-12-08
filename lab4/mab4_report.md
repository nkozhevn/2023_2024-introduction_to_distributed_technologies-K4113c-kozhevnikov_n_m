University: [ITMO University](https://itmo.ru/ru/)\
Faculty: [FICT](https://fict.itmo.ru)\
Course: [Introduction to distributed technologies](https://github.com/itmo-ict-faculty/introduction-to-distributed-technologies)\
Year: 2023/2024\
Group: K4113c\
Author: Kozhevnikov Nikolai Mikhailovich\
Lab: Lab4\
Date of create: 08.11.2023\
Date of finished: 

___

### Подготовка ПО
1. Запуск minikube с плагином сalico и двумя нодами
```
minikube start --network-plugin=cni --cni=calico --nodes 2
```
<img width="568" alt="image" src="https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/c4155ecd-7989-443a-bfa0-f91a8b66fae9">

2. Установка calicoctl
```
kubectl create -f calicoctl.yaml
```
<img width="571" alt="image" src="https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/6851864e-fdb1-4634-a7c1-c84b9438ca0f">

3. Проверка нод и подов calico
```
kubectl get nodes
```
<img width="429" alt="image" src="https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/40d946bf-27e1-4424-85d5-d2f1ad58063d">\
```
kubectl get pods -l k8s-app=calico-node -A
```
<img width="569" alt="image" src="https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/d4d4007f-fe80-4448-b4e2-1ead6e8c1830">

### Работа с нодами
1. Установка label для нод
```
kubectl label nodes minikube zone=home 
kubectl label nodes minikube-m02 zone=work
```
<img width="567" alt="image" src="https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/d4c2db1f-6197-4071-bea5-463ef077cd85">

2. Удаление созданных по умолчанию IPPools
```
kubectl exec -i -n kube-system calicoctl -- /calicoctl --allow-version-mismatch get ippools -o wide
```
<img width="569" alt="image" src="https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/7f4c0041-9d42-44eb-909c-823beb14b99b">\
```
kubectl delete ippools default-ipv4-ippool
```
<img width="570" alt="image" src="https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/4a73d0be-a4fa-4375-b653-d86c8c167334">

3. Манифест для создания IPPools
```
apiVersion: projectcalico.org/v3
kind: IPPool
metadata:
   name: zone-home-ippool
spec:
   cidr: 192.168.0.0/24
   ipipMode: Always
   natOutgoing: true
   nodeSelector: zone == "home"
---
apiVersion: projectcalico.org/v3
kind: IPPool
metadata:
   name: zone-work-ippool
spec:
   cidr: 192.168.1.0/24
   ipipMode: Always
   natOutgoing: true
   nodeSelector: zone == "work"
```
В манифесте указаны IP-адреса и значения переменных для IPPools.

4. Применение манифеста
```
kubectl exec -i -n kube-system calicoctl -- /calicoctl --allow-version-mismatch create -f - < /Users/nikolai_kozevnikov/Desktop/IP-Pools.yaml
```
<img width="567" alt="image" src="https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/a7c85441-9801-4d1a-ad00-4c5155659af7">\
```
kubectl exec -i -n kube-system calicoctl -- /calicoctl --allow-version-mismatch get ippool -o wide   
```
<img width="568" alt="image" src="https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/05340670-3cac-4017-a335-37c3618e7bf8">

### Запуск контейнеров
1. Манифест deployment
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: deployment
  labels:
    app: frontend
spec:
  replicas: 2
  selector:
    matchLabels:
      app: frontend
  template:
    metadata:
      labels:
        app: frontend
    spec:
      containers:
      - name: frontend-container
        image: ifilyaninitmo/itdt-contained-frontend:master
        ports:
        - containerPort: 3000
        env:
        - name: REACT_APP_USERNAME
          value: "kkolyambuss"
        - name: REACT_APP_COMPANY_NAME
          value: "home"

---

apiVersion: v1
kind: Service
metadata:
  name: service
spec:
  selector:
    app: frontend
  ports:
    - port: 3000
      targetPort: 3000
  type: LoadBalancer
```
В манифесте прописано создание Deployment и Service.

2. Применение манифеста
```
kubectl apply -f /Users/nikolai_kozevnikov/Desktop/Pools-Deployment.yaml
```
<img width="566" alt="image" src="https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/27bff197-d73a-4311-9e12-64c08d10fd72">

3. Просмотр информации о подах
```
kubectl get pods -o wide
```
<img width="566" alt="image" src="https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/45ee2578-f419-4ef7-b2e5-6b9e42718dd4">

### Просмотр результатов
1. Проброс портов и просмотр страницы
```
kubectl port-forward service/service 8200:3000  
```
<img width="1406" alt="image" src="https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/51fe1059-45f8-4fb1-88e3-7ba9322587dd">\
Значения переменных, прописанные в манифесте, остаются неизменными. Имя пода и IP-адрес могут меняться в зависимости от того, к какому поду было выполнено подключение.

2. ping соседних подов
```
kubectl exec -ti deployment-6fbd69cfbd-drx5r -- sh
```
```
ping 192.168.0.65
```
<img width="564" alt="image" src="https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/d2177993-3070-40fa-880e-4bad8ce97b50">\
```
kubectl exec -ti deployment-6fbd69cfbd-hxxf7 -- sh
```
```
ping 192.168.1.0
```
<img width="568" alt="image" src="https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/51129a34-2e5b-4e24-b4be-e19fc5cd4bfd">

___

### Схема организации контейнеров
<img width="384" alt="image" src="https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/d2559a0a-5bda-410b-900a-cc15bff753cd">
