### Установка ПО
1. Установка Docker
2. Запуск minikube
```
minikube start
```
<img width="568" alt="image" src="https://github.com/nkozhevn/introduction_to_distributed_technologies_labs/assets/74055661/bcacacc0-36ea-4764-a1cc-9d6d294da43e">

3. Установка kubectl
```
minikube kubectl
```
<img width="568" alt="image" src="https://github.com/nkozhevn/introduction_to_distributed_technologies_labs/assets/74055661/666c2bed-143a-4731-99a7-22e2f940560a">

### Использование манифеста
1. Манифест для для развертывания пода
```
apiVersion: v1
kind: Pod
metadata:
  name: vault
  namespace: default
  labels:
    app: vault
spec:
  containers:
  - name: vault
    image: hashicorp/vault
    ports:
      - containerPort: 8200
```
В манифесте прописан образ hashicorp/vault, на основе которого создан под vault, а также порт 8200, который прокидывается внутрь.

2. Применение манифеста
```
minikube kubectl -- apply -f /Users/nikolai_kozevnikov/Desktop/Vault-Pod.yaml
```
<img width="568" alt="image" src="https://github.com/nkozhevn/introduction_to_distributed_technologies_labs/assets/74055661/3ea20eab-8a25-42c5-a9ea-549a3a3d4c1b">

3. Создание сервиса для доступа к поду
```
minikube kubectl -- expose pod vault --type=NodePort --port=8200
```
<img width="563" alt="image" src="https://github.com/nkozhevn/introduction_to_distributed_technologies_labs/assets/74055661/870bbfc1-fca8-4cb9-99d7-b98c03322535">

### Просмотр контейнера
1. Просмотр логов
```
minikube kubectl -- logs vault
```
<img width="515" alt="image" src="https://github.com/nkozhevn/introduction_to_distributed_technologies_labs/assets/74055661/70061f4a-6ea8-4b18-bb8a-ff5a7df1191e">
В логах видно Root Token - он нужен для входа в vault.

2. Проброс портов
```
minikube kubectl -- port-forward service/vault 8200:8200
```
<img width="567" alt="image" src="https://github.com/nkozhevn/introduction_to_distributed_technologies_labs/assets/74055661/b7e7053d-ab06-470d-8bb8-36ddee991e3e">

3. Отображаемая страница после входа
<img width="1403" alt="image" src="https://github.com/nkozhevn/introduction_to_distributed_technologies_labs/assets/74055661/ee91075c-7135-4500-bcce-1cee59323a25">

4. Завершение работы с minikube
```
minikube stop
```
<img width="568" alt="image" src="https://github.com/nkozhevn/introduction_to_distributed_technologies_labs/assets/74055661/d06374bd-6480-4208-a23b-ffad92497e4c">

### Схема организации контейнеров
![containers](https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/d61bdf6f-4745-4ee0-b1ac-6567a6ab5a76)
