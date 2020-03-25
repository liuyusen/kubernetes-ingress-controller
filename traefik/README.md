1. Install traefik 2.0
wget https://get.helm.sh/helm-v3.1.2-linux-amd64.tar.gz
tar -zxvf helm-v3.1.2-linux-amd64.tar.gz
mv linux-amd64/helm /usr/local/bin/helm
git clone https://github.com/containous/traefik-helm-chart
helm install ./traefik-helm-chart/traefik --generate-name

kubectl edit deployment traefik
Add the following arg to container args of traefik deployment:
--providers.kubernetesIngress

2. Install Sample
kubectl apply -f ./kubernetes-ingress-controller/traefik/samples/simple.yaml

3. Verification
vi /etc/hosts and add
<Your ingress controller IP> ingress1.test.cn
<Your ingress controller IP> simpleingressroute.test.cn

curl ingress1.test.cn
curl simpleingressroute.test.cn
curl simpleingressroute.test.cn -H "Eason:yes"
