'''
minikube start
'''
<img width="568" alt="image" src="https://github.com/nkozhevn/introduction_to_distributed_technologies_labs/assets/74055661/bcacacc0-36ea-4764-a1cc-9d6d294da43e">

'''
minikube kubectl
'''
<img width="568" alt="image" src="https://github.com/nkozhevn/introduction_to_distributed_technologies_labs/assets/74055661/666c2bed-143a-4731-99a7-22e2f940560a">


применение манифеста
'''
minikube kubectl -- apply -f /Users/nikolai_kozevnikov/Desktop/Vault-Pod.yaml
'''
<img width="568" alt="image" src="https://github.com/nkozhevn/introduction_to_distributed_technologies_labs/assets/74055661/3ea20eab-8a25-42c5-a9ea-549a3a3d4c1b">

'''
minikube kubectl -- expose pod vault --type=NodePort --port=8200
'''
<img width="563" alt="image" src="https://github.com/nkozhevn/introduction_to_distributed_technologies_labs/assets/74055661/870bbfc1-fca8-4cb9-99d7-b98c03322535">

'''
minikube kubectl -- logs vault
'''
<img width="515" alt="image" src="https://github.com/nkozhevn/introduction_to_distributed_technologies_labs/assets/74055661/70061f4a-6ea8-4b18-bb8a-ff5a7df1191e">

'''
minikube kubectl -- port-forward service/vault 8200:8200
'''
<img width="567" alt="image" src="https://github.com/nkozhevn/introduction_to_distributed_technologies_labs/assets/74055661/b7e7053d-ab06-470d-8bb8-36ddee991e3e">

Результат
<img width="1403" alt="image" src="https://github.com/nkozhevn/introduction_to_distributed_technologies_labs/assets/74055661/ee91075c-7135-4500-bcce-1cee59323a25">

'''
minikube stop
'''
<img width="568" alt="image" src="https://github.com/nkozhevn/introduction_to_distributed_technologies_labs/assets/74055661/d06374bd-6480-4208-a23b-ffad92497e4c">

