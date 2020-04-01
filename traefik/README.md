Use Cases:
Different use cases should be tested on separate clusters.

1. Run 1.7 and 2.1 at the same time
1.1 Install traefik
kubectl apply -f ./kubernetes-ingress-controller/traefik/1.7/namespace.yaml
kubectl apply -f ./kubernetes-ingress-controller/traefik/1.7/

kubectl apply -f ./kubernetes-ingress-controller/traefik/2.1/rbac/namespace.yaml
kubectl apply -f ./kubernetes-ingress-controller/traefik/2.1/rbac/
kubectl apply -f ./kubernetes-ingress-controller/traefik/2.1/crds/
kubectl apply -f ./kubernetes-ingress-controller/traefik/2.1/

1.2 Install Sample
kubectl apply -f ./kubernetes-ingress-controller/traefik/samples/simple.yaml

1.3 Verification
Get ingress controller IP:
kubectl get service traefik-ingress-service -n traefik-1-7
vi /etc/hosts and add
<Your ingress controller IP> ingress1.test.cn

kubectl get service traefik-ingress-service -n traefik-2-1
vi /etc/hosts and add
<Your ingress controller IP> simpleingressroute.test.cn

curl ingress1.test.cn
curl simpleingressroute.test.cn
curl simpleingressroute.test.cn -H "Eason:yes"
curl simpleingressroute.test.cn -H "Source:I'm Ray"
curl simpleingressroute.test.cn -H "Source:I'm Eason"
curl simpleingressroute.test.cn -H "Source:I'm Steven"

1.4 Uninstall
kubectl delete -f ./kubernetes-ingress-controller/traefik/samples/simple.yaml
kubectl delete -f ./kubernetes-ingress-controller/traefik/1.7/
kubectl delete -f ./kubernetes-ingress-controller/traefik/1.7/namespace.yaml

kubectl delete -f ./kubernetes-ingress-controller/traefik/2.1/
kubectl delete -f ./kubernetes-ingress-controller/traefik/2.1/rbac/
kubectl delete -f ./kubernetes-ingress-controller/traefik/2.1/rbac/namespace.yaml
kubectl delete -f ./kubernetes-ingress-controller/traefik/2.1/crds/

2. Run 2.2 only
2.1 Install traefik
#wget https://get.helm.sh/helm-v3.1.2-linux-amd64.tar.gz
#tar -zxvf helm-v3.1.2-linux-amd64.tar.gz
#mv linux-amd64/helm /usr/local/bin/helm
#git clone https://github.com/containous/traefik-helm-chart
#helm install traefik-2-0 ./traefik-helm-chart/traefik --set="image.tag=2.0,additionalArguments={--providers.kubernetesingress,--providers.kubernetesingress.ingressclass=traefik-2.0}"

kubectl apply -f ./kubernetes-ingress-controller/traefik/2.2/rbac/namespace.yaml
kubectl apply -f ./kubernetes-ingress-controller/traefik/2.2/rbac/
kubectl apply -f ./kubernetes-ingress-controller/traefik/2.2/crds/
kubectl apply -f ./kubernetes-ingress-controller/traefik/2.2/

2.2 Install Sample
kubectl apply -f ./kubernetes-ingress-controller/traefik/samples/2.2.yaml

2.3 Verification
Get ingress controller IP:
kubectl get service traefik-ingress-service -n traefik-2-2
vi /etc/hosts and add
<Your ingress controller IP> ingress1.test.cn
<Your ingress controller IP> simpleingressroute.test.cn

curl ingress1.test.cn
curl simpleingressroute.test.cn
curl simpleingressroute.test.cn -H "Eason:yes"
curl simpleingressroute.test.cn -H "Source:I'm Ray"
curl simpleingressroute.test.cn -H "Source:I'm Eason"
curl simpleingressroute.test.cn -H "Source:I'm Steven"

2.4 Uninstall
kubectl delete -f ./kubernetes-ingress-controller/traefik/samples/2.2.yaml

kubectl delete -f ./kubernetes-ingress-controller/traefik/2.2/
kubectl delete -f ./kubernetes-ingress-controller/traefik/2.2/rbac/
kubectl delete -f ./kubernetes-ingress-controller/traefik/2.2/rbac/namespace.yaml
kubectl delete -f ./kubernetes-ingress-controller/traefik/2.2/crds/