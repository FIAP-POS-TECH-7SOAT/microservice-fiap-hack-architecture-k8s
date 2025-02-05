aws eks update-kubeconfig --region us-east-1 --name hack-fiap      

-> install ingress no cluster

helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx

-> install grafana no cluster

helm repo add grafana https://grafana.github.io/helm-charts

helm repo update

helm upgrade --install --values loki-stack-configs.yaml loki grafana/loki-stack
helm install ingress-nginx ingress-nginx/ingress-nginx --namespace ingress-nginx --create-namespace
<!-- helm install grafana grafana/grafana --namespace grafana --create-namespace -->

<!-- Pegar senha do grafana -->
kubectl get secret  loki-grafana -o jsonpath="{.data.admin-password}" | foreach { [System.Text.Encoding]::UTF8.GetString([Convert]::FromBase64String($_)) }
asg0J7n4draYzn8vaPimcxJvCy0NN5OanDNc8Fsv

<!-- Verify nginx -->
kubectl get pods -n ingress-nginx
kubectl get svc -n ingress-nginx

<!-- comandos -->

kubectl get pods 
kubectl logs hack-send-videos-deployment-7bbfcb656b-r4tjr  
kubectl describe hack-send-videos-deployment-7bbfcb656b-r4tjr  


<!-- install configs -->
kubectl apply -f .\config-map
kubectl apply -f .\microservice-redis-component.yml

<!-- kubectl create namespace monitoring -->
<!-- kubectl apply -f .\shared-logs-persist-volume.yml -->

kubectl apply -f .\microservice-hack-authentication-deployment.yml
kubectl apply -f .\microservice-hack-authentication-service.yml

kubectl apply -f .\microservice-hack-notification-deployment.yml
<!-- kubectl apply -f .\microservice-hack-notification-service.yml    -->


kubectl apply -f .\microservice-hack-send-videos-deployment.yml
kubectl apply -f .\microservice-hack-send-videos-service.yml

kubectl apply -f .\microservice-hack-process-videos-deployment.yml

kubectl apply -f .\ingress.controller.yml


<!-- unistall configs -->
kubectl delete -f .\config-map   
kubectl delete -f .\microservice-hack-authentication-deployment.yml
kubectl delete -f .\microservice-hack-authentication-service.yml   

kubectl delete -f .\microservice-hack-notification-deployment.yml
kubectl delete -f .\microservice-hack-notification-service.yml   

kubectl delete -f .\microservice-hack-send-videos-deployment.yml
kubectl delete -f .\microservice-hack-send-videos-service.yml   
kubectl delete -f .\ingress.controller.yml


<!-- back to your k8s local configuration -->
kubectl config use-context docker-desktop  




helm repo add grafana https://grafana.github.io/helm-charts
helm repo update
kubectl apply -f .\config-map 
kubectl apply -f .\shared-logs-persist-volume.yml

<!-- Pegar senha do grafana -->
kubectl get secret  loki-grafana -o jsonpath="{.data.admin-password}" | foreach { [System.Text.Encoding]::UTF8.GetString([Convert]::FromBase64String($_)) }

kubectl port-forward loki-grafana-7d88946c97-fmj87   9090:3000  
kubectl port-forward hack-authentication-deployment-86cd848bbb-84fwq   3333:3333 

kubectl apply -f promtail-deployment.yaml 
kubectl delete -f microservice-hack-send-videos-deployment.yml 


https://www.youtube.com/watch?v=O52dseg2bJo&t=686s


