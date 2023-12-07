minikube start
<img width="565" alt="image" src="https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/7514636c-f52f-47ff-8feb-025a34a76866">

docker pull ifilyaninitmo/itdt-contained-frontend:master
<img width="566" alt="image" src="https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/0f13b5fe-09d7-4582-886c-8c23920c114a">

minikube addons enable ingress
<img width="568" alt="image" src="https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/545ba30f-af9a-474d-9f39-6027748ba12d">

openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout tls.key -out tls.crt -subj "/CN=react.secret"
<img width="569" alt="image" src="https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/faa24ecd-1661-4cd5-8828-6ce17ed8ff09">

kubectl create secret tls secret-tls --key="tls.key" --cert="tlscrt"
<img width="567" alt="image" src="https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/c74e10f9-1a16-4f27-8715-d7ed9e5e368f">

kubectl apply -f /Users/nikolai_kozevnikov/Desktop/Secret-App.yaml
<img width="568" alt="image" src="https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/81453cd8-a3ab-4f56-a88d-ff3a4317fb42">

sudo nano /etc/hosts
127.0.0.1       react.secret
<img width="562" alt="image" src="https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/cb2d9dc1-8c9d-401f-bfab-33fed2d31da7">

react.secret
<img width="538" alt="image" src="https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/4d56f5a6-6338-4315-845c-fc304d172a67">

<img width="400" alt="image" src="https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/62e84202-35ed-4cbd-84fc-f9c5a825dfa5">

