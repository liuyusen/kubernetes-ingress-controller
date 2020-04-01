1. Install traefik 2.x
#wget https://get.helm.sh/helm-v3.1.2-linux-amd64.tar.gz
#tar -zxvf helm-v3.1.2-linux-amd64.tar.gz
#mv linux-amd64/helm /usr/local/bin/helm
#git clone https://github.com/containous/traefik-helm-chart
#helm install traefik-2-0 ./traefik-helm-chart/traefik --set="image.tag=2.0,additionalArguments={--providers.kubernetesingress,--providers.kubernetesingress.ingressclass=traefik-2.0}"

kubectl apply -f ./kubernetes-ingress-controller/traefik/1.7/namespace.yaml
kubectl apply -f ./kubernetes-ingress-controller/traefik/1.7/

kubectl apply -f ./kubernetes-ingress-controller/traefik/2.1/rbac/namespace.yaml
kubectl apply -f ./kubernetes-ingress-controller/traefik/2.1/rbac/
kubectl apply -f ./kubernetes-ingress-controller/traefik/2.1/crds/
kubectl apply -f ./kubernetes-ingress-controller/traefik/2.1/

2. Install Sample
kubectl apply -f ./kubernetes-ingress-controller/traefik/samples/simple.yaml

3. Verification
Get ingress controller IP:
kubectl get service traefik-1-7
vi /etc/hosts and add
<Your ingress controller IP> ingress1.test.cn

kubectl get service traefik-2-1
vi /etc/hosts and add
<Your ingress controller IP> simpleingressroute.test.cn

curl ingress1.test.cn
curl simpleingressroute.test.cn
curl simpleingressroute.test.cn -H "Eason:yes"
curl simpleingressroute.test.cn -H "Source:I'm Ray"
curl simpleingressroute.test.cn -H "Source:I'm Eason"
curl simpleingressroute.test.cn -H "Source:I'm Steven"