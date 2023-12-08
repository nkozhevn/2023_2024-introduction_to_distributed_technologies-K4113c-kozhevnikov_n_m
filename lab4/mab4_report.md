minikube start --network-plugin=cni --cni=calico --nodes 2
<img width="568" alt="image" src="https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/c4155ecd-7989-443a-bfa0-f91a8b66fae9">

kubectl get nodes
<img width="429" alt="image" src="https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/40d946bf-27e1-4424-85d5-d2f1ad58063d">

kubectl get pods -l k8s-app=calico-node -A
<img width="569" alt="image" src="https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/d4d4007f-fe80-4448-b4e2-1ead6e8c1830">

<img width="988" alt="image" src="https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/1ddff8ee-032e-4402-9c3c-01724b62b244">

kubectl label nodes minikube zone=home 
kubectl label nodes minikube-m02 zone=work
<img width="567" alt="image" src="https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/d4c2db1f-6197-4071-bea5-463ef077cd85">

kubectl create -f calicoctl.yaml
<img width="571" alt="image" src="https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/6851864e-fdb1-4634-a7c1-c84b9438ca0f">

kubectl exec -i -n kube-system calicoctl -- /calicoctl --allow-version-mismatch get ippools -o wide
<img width="569" alt="image" src="https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/7f4c0041-9d42-44eb-909c-823beb14b99b">

kubectl delete ippools default-ipv4-ippool
<img width="570" alt="image" src="https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/4a73d0be-a4fa-4375-b653-d86c8c167334">

kubectl exec -i -n kube-system calicoctl -- /calicoctl --allow-version-mismatch create -f - < /Users/nikolai_kozevnikov/Desktop/IP-Pools.yaml
<img width="567" alt="image" src="https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/a7c85441-9801-4d1a-ad00-4c5155659af7">

kubectl exec -i -n kube-system calicoctl -- /calicoctl --allow-version-mismatch get ippool -o wide   
<img width="568" alt="image" src="https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/05340670-3cac-4017-a335-37c3618e7bf8">

kubectl apply -f /Users/nikolai_kozevnikov/Desktop/Pools-Deployment.yaml
<img width="566" alt="image" src="https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/27bff197-d73a-4311-9e12-64c08d10fd72">

kubectl get pods -o wide
<img width="566" alt="image" src="https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/45ee2578-f419-4ef7-b2e5-6b9e42718dd4">

kubectl port-forward service/service 8200:3000  
<img width="1406" alt="image" src="https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/51fe1059-45f8-4fb1-88e3-7ba9322587dd">

kubectl exec -ti deployment-6fbd69cfbd-drx5r -- sh
ping 192.168.0.65
<img width="564" alt="image" src="https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/d2177993-3070-40fa-880e-4bad8ce97b50">

kubectl exec -ti deployment-6fbd69cfbd-hxxf7 -- sh
ping 192.168.1.0
<img width="568" alt="image" src="https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/51129a34-2e5b-4e24-b4be-e19fc5cd4bfd">

<img width="384" alt="image" src="https://github.com/nkozhevn/2023_2024-introduction_to_distributed_technologies-K4113c-kozhevnikov_n_m/assets/74055661/d2559a0a-5bda-410b-900a-cc15bff753cd">

