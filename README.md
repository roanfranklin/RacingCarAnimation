### RacingCarAnimation

HTML Animado com JS para imagem Docker com manifestos base para funcionamento em Kubernetes.

### 🛠 Lista Comandos

1º Iniciar o minkube com o comando:

```bash
minikube start --driver=none
```

2º Ativa o modulo de metricas para funcionamento do HPA - HorizontalPodAutoescaler:

```bash
minikube addons enable metrics-server
```

3º Ativa o modulo ingress para uso de uma entrada como Load Balancer:

```bash
minikube addons enable ingress
```

4º O Ingress foi carregado, porém ao dar um describe para ver as configurações do mesmo, aparece um erro de redirecioanamento. Então para funcionar é só carregar os dois manifestos abaixo.
```bash
kubectl apply -f https://raw.githubusercontent.com/roelal/minikube/5093d8b21c0931a6c63fa448538761b4bf100ee0/deploy/addons/ingress/ingress-rc.yaml
kubectl apply -f https://raw.githubusercontent.com/roelal/minikube/5093d8b21c0931a6c63fa448538761b4bf100ee0/deploy/addons/ingress/ingress-svc.yaml
```

5º Iremos criar a imagem que será usada para levantar a aplicação pelo k8s:

```bash
docker build -t roanfranklin/racingcaranimation:1.0.0 .
```

6º Aplicar os manifestos da aplicação:

```bash
kubectl apply -f k8s/namespace.yaml
kubectl apply -f k8s/deployment.yaml
kubectl apply -f k8s/hpa.yaml
kubectl apply -f k8s/service.yaml
```

7º Monitoramento - Alguns comandos:

```bash
kubectl get all --all-namespaces

kubectl get deploy,pods,svc,hpa,ing -n hml

kubectl get deploy,pods,svc,hpa,ing -n hml -o wide

watch -n1 "kubectl get deploy,pods,svc,hpa,ing -n hml -o wide"
```
