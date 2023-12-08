University: [ITMO University](https://itmo.ru/ru/)\
Faculty: [FICT](https://fict.itmo.ru)\
Course: [Introduction to distributed technologies](https://github.com/itmo-ict-faculty/introduction-to-distributed-technologies)\
Year: 2023/2024\
Group: K4113c\
Author: Kozhevnikov Nikolai Mikhailovich\
Lab: Lab3\
Date of create: 06.12.2023\
Date of finished: 

___

### Подготовка ПО
1. Запуск minikube
```
minikube start
```
<img width="565" alt="image" src="https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/7514636c-f52f-47ff-8feb-025a34a76866">

2. Включение ingress
```
minikube addons enable ingress
```
<img width="568" alt="image" src="https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/545ba30f-af9a-474d-9f39-6027748ba12d">

### Работа с сертефикатом
1. Генерация сертефиката
```
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout tls.key -out tls.crt -subj "/CN=react.secret"
```
<img width="569" alt="image" src="https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/faa24ecd-1661-4cd5-8828-6ce17ed8ff09">

<img width="567" alt="image" src="https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/c74e10f9-1a16-4f27-8715-d7ed9e5e368f">

2. Создание манифеста
```
apiVersion: v1
kind: ConfigMap
metadata:
  name: react-app-variables
data:
  REACT_APP_USERNAME: "kkolyambuss"
  REACT_APP_COMPANY_NAME: "home"

---

apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: react
  labels:
    app: react
spec:
  replicas: 2
  selector:
    matchLabels:
      app: react
  template:
    metadata:
      labels:
        app: react
    spec:
      containers:
        - name: react
          image: ifilyaninitmo/itdt-contained-frontend:master
          ports:
            - containerPort: 3000
          env:
            - name: REACT_APP_USERNAME
              valueFrom:
                configMapKeyRef:
                  name: react-app-variables
                  key: REACT_APP_USERNAME
            - name: REACT_APP_COMPANY_NAME
              valueFrom:
                configMapKeyRef:
                  name: react-app-variables
                  key: REACT_APP_COMPANY_NAME

---

apiVersion: v1
kind: Service
metadata:
  name: react
spec:
  type: NodePort
  ports:
    - port: 3000
      targetPort: 3000
      protocol: TCP
  selector:
    app: replica-set-react

---

apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: my-ingress
spec:
  tls:
  - hosts:
    - react.secret
    secretName: tls-secret
  rules:
  - host: react.secret
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: react
            port:
              number: 3000
```
В манифесте создается ConfigMap с нужными переменными, ReplicaSet и Service. В нем же создается ingress с указанием созданных ключей и пути.

3. Применение манифеста
```
kubectl apply -f /Users/nikolai_kozevnikov/Desktop/Secret-App.yaml
```
<img width="568" alt="image" src="https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/81453cd8-a3ab-4f56-a88d-ff3a4317fb42">

### Просмотр результата
1. Запись доменного имени в hosts
```
sudo nano /etc/hosts
```
```
127.0.0.1       react.secret
```
<img width="562" alt="image" src="https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/cb2d9dc1-8c9d-401f-bfab-33fed2d31da7">

2. Просмотр сертефиката по доменному имени
```
react.secret
```
<img width="400" alt="image" src="https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/62e84202-35ed-4cbd-84fc-f9c5a825dfa5">

### Схема организации контейнеров
![image](https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/b151e7be-87b5-49d4-9a22-34397932ca62)
