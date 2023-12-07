minikube start --network-plugin=cni --cni=calico --nodes 2
<img width="568" alt="image" src="https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/c4155ecd-7989-443a-bfa0-f91a8b66fae9">

kubectl get pods -w -l k8s-app=calico-node -A
<img width="567" alt="image" src="https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/7d70bcc2-88b2-4669-9509-5a2531eb5acf">

<img width="988" alt="image" src="https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/1ddff8ee-032e-4402-9c3c-01724b62b244">

kubectl label nodes minikube company=home 
kubectl label nodes minikube-m02 company=work
<img width="565" alt="image" src="https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/01b3aa81-a2be-4e1a-b45e-0a1599657112">


