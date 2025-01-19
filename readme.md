aws eks update-kubeconfig --region us-east-1 --name hack-fiap      

-> install ingress no cluster

helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update
helm install ingress-nginx ingress-nginx/ingress-nginx --namespace ingress-nginx --create-namespace


<!-- Verify nginx -->
kubectl get pods -n ingress-nginx
kubectl get svc -n ingress-nginx

<!-- install configs -->
kubectl apply -f .\config-map
kubectl apply -f .\lmicroservice-hack-notification-deployment.yml
kubectl apply -f .\lmicroservice-hack-notification-service.yml   
kubectl apply -f .\microservice-hack-send-videos-deployment.yml
kubectl apply -f .\microservice-hack-send-videos-service.yml
kubectl apply -f .\ingress.controller.yml


<!-- unistall configs -->
kubectl delete -f .\config-map   
kubectl delete -f .\lmicroservice-hack-notification-deployment.yml
kubectl delete -f .\lmicroservice-hack-notification-service.yml   
kubectl delete -f .\microservice-hack-send-videos-deployment.yml
kubectl delete -f .\microservice-hack-send-videos-service.yml   
kubectl delete -f .\ingress.controller.yml


<!-- back to your k8s local configuration -->
kubectl config use-context docker-desktop  