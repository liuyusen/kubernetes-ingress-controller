1. Install nginx ingress controller
kubectl apply -f ./kubernetes-ingress-controller/ingress-nginx/0.30.0/mandatory.yaml
kubectl apply -f ./kubernetes-ingress-controller/ingress-nginx/0.30.0/service-nodeport.yaml

2. Install Sample
kubectl apply -f ./kubernetes-ingress-controller/ingress-nginx/samples/simple.yaml

3. Verification
Get ingress controller IP:
kubectl get service ingress-nginx -n ingress-nginx
vi /etc/hosts and add
<Your ingress controller IP> ingress-nginx.test.cn

curl ingress-nginx.test.cn
curl ingress-nginx.test.cn -H "Source:Michael"
curl ingress-nginx.test.cn -H "Source:I'm Eason"
curl ingress-nginx.test.cn -H "Source:I'm Steven"

kubectl apply -f ./kubernetes-ingress-controller/ingress-nginx/samples/weight.yaml
curl ingress-nginx.test.cn
curl ingress-nginx.test.cn -H "Source:Michael"
curl ingress-nginx.test.cn -H "Source:I'm Eason"
curl ingress-nginx.test.cn -H "Source:I'm Steven"

4. Uninstall
kubectl delete -f ./kubernetes-ingress-controller/ingress-nginx/samples/simple.yaml
kubectl delete -f ./kubernetes-ingress-controller/ingress-nginx/0.30.0/service-nodeport.yaml
kubectl delete -f ./kubernetes-ingress-controller/ingress-nginx/0.30.0/mandatory.yaml
