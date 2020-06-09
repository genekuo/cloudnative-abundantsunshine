redis-cli -h $(minikube service redis-svc --url --format "{{.IP}}") -p $(minikube service redis-svc --url --format "{{.Port}}")

minikube service redis-svc --url --format "{{.IP}}"
minikube service redis-svc --url --format "{{.Port}}"

curl -i $(minikube service --url connectionsposts-svc)/connectionsposts
curl -X POST -i -c cookie -d "username=cdavisafc" $(minikube service --url connectionsposts-svc)/login
curl -i -b cookie $(minikube service --url connectionsposts-svc)/connectionsposts

kubectl scale --replicas=2 deployment.apps/connectionsposts
