start :
	minikube start --registry-mirror=https://registry.docker-cn.com --vm-driver=hyperkit --kubernetes-version v1.17.0 --alsologtostderr
	# --extra-config=controller-manager.ClusterSigningCertFile="/Users/Arthur/.minikube/certs/ca.pem"
	# --extra-config=controller-manager.ClusterSigningKeyFile="/Users/Arthur/.minikube/certs/ca-key.pem"
	@eval $(minikube docker-env)
	kubectl config use-context minikube
	minikube addons enable coredns
	minikube addons enable heapster
	minikube addons enable metrics-server
	minikube addons enable freshpod
addons:
	minikube addons enable coredns
	minikube addons enable heapster
	minikube addons enable metrics-server
	minikube addons enable freshpod
restart :
	minikube stop
	minikube start --registry-mirror=https://registry.docker-cn.com --vm-driver=hyperkit  --kubernetes-version v1.11.0 --alsologtostderr 
	kubectl config use-context minikube
	minikube dashboard
clean :
	@rm -rf ~/.minikube
stop :
	minikube stop
list : 
	minikube addons list
install :
	## Just for mac
	## curl -Lo minikube http://kubernetes.oss-cn-hangzhou.aliyuncs.com/minikube/releases/v0.23.0/minikube-darwin-amd64 && chmod +x minikube && sudo mv minikube /usr/local/bin/
	brew cask install minikube
ssh :
	minikube ssh
	# docker pull hub.c.163.com/allan1991/pause-amd64:3.0
	# docker tag hub.c.163.com/allan1991/pause-amd64:3.0 gcr.io/google_containers/pause-amd64:3.0
busybox:
	kubectl run busybox --image=busybox 
test-dns: busybox
	kubectl exec -ti busybox -- nslookup kubernetes.default
show:
	cd ppt && bs serve
cleanK8sObj:
	kubectl delete $(kubectl get persistentvolume -o name)
	kubectl delete $(kubectl get deployment -o name)
	kubectl delete $(kubectl get replicationcontroller -o name)
	kubectl delete $(kubectl get cronjob -o name)
	kubectl delete $(kubectl get svc -o name)
	kubectl delete $(kubectl get po -o name)
	kubectl delete $(kubectl get jobs -o name)
