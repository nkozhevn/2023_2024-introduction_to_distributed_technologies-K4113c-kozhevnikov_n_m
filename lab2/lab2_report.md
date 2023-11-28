
``
kubectl apply -f /Users/nikolai_kozevnikov/Desktop/App-Deployment.yaml
``
<img width="567" alt="image" src="https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/1bd614e9-3571-45b4-8d10-1fb3d6f10f87">

``
docker pull ifilyaninitmo/itdt-contained-frontend:master
``
<img width="565" alt="image" src="https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/310c0758-4363-432e-a1bc-d63e0782aef4">

Команда не работает
``
minikube kubectl port-forward service/app 3000:3000 -n default
``
<img width="568" alt="image" src="https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/cabde5bc-f8a9-4057-a74c-c8638e9d813e">

Используем эту
``
minikube kubectl get pods
``
<img width="539" alt="image" src="https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/28dedffd-8708-4fbc-96e3-f447d62a9071">

``
minikube kubectl port-forward app-5dd85f6759-2d9qx 3000:3000
``
<img width="567" alt="image" src="https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/5e580fa8-e33a-464e-89b6-6ca8b9bd8a69">

Открытая страница
<img width="1400" alt="image" src="https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/d7c0e6df-451e-4d17-9df5-f4c32d4073a9">

``
minikube kubectl logs app-5dd85f6759-2d9qx
``
<img width="567" alt="image" src="https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/c470f986-df00-4730-bf7d-cf4235216d77">

``
minikube kubectl logs app-5dd85f6759-2lt6d
``
<img width="568" alt="image" src="https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/2f60581f-79ca-48a7-abc4-a1640098e5ec">


![deployment](https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/58809d04-cb40-4dc0-a3b0-8e0bdfd19ccf)

