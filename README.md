This repository contains the source files needed to follow the series [Kubernetes and everything else](https://rinormaloku.com/series/kubernetes-and-everything-else/) or summarized as an article in [Learn Kubernetes in Under 3 Hours: A Detailed Guide to Orchestrating Containers](https://medium.freecodecamp.org/learn-kubernetes-in-under-3-hours-a-detailed-guide-to-orchestrating-containers-114ff420e882)

To learn more about Kubernetes and other related topics check the following examples with the **Sentiment Analysis** application:

* [Kubernetes Volumes in Practice](https://rinormaloku.com/kubernetes-volumes-in-practice/):
* [Ingress Controller - simplified routing in Kubernetes](https://www.orange-networks.com/blogs/210-ingress-controller-simplified-routing-in-kubernetes)
* [Docker Compose in Practice](https://github.com/rinormaloku/k8s-mastery/tree/docker-compose)
* [Istio around everything else series](https://rinormaloku.com/series/istio-around-everything-else/)
* [Simple CI/CD for Kubernetes with Azure DevOps](https://www.orange-networks.com/blogs/224-azure-devops-ci-cd-pipeline-to-deploy-to-kubernetes)
* Envoy series - to be added!


Usage:
docker build -f Dockerfile -t sentiment-analysis-frontend .
docker build -f Dockerfile -t sentiment-analysis-web-app .
docker build -f Dockerfile -t sentiment-analysis-logic .

docker run -d -p 8888:80   --name=front sentiment-analysis-frontend
docker run -d -p 8080:8080 --name=web   sentiment-analysis-web-app
docker run -d -p 5000:5000 --name=logic sentiment-analysis-logic


installing cubectl:
1) manualy
curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl
kubectl version --client

sudo apt-get install qemu-kvm libvirt-bin virtinst bridge-utils cpu-checker
kvm-ok
sudo cp /etc/network/interfaces /etc/network/interfaces.bakup-1-july-2016
sudo vi /etc/network/interfaces
edit append:
auto br0
 iface br0 inet static
         address 10.18.44.26
         netmask 255.255.255.192
         broadcast 10.18.44.63
         dns-nameservers 10.0.80.11 10.0.80.12
         # set static route for LAN
 	 post-up route add -net 10.0.0.0 netmask 255.0.0.0 gw 10.18.44.1
 	 post-up route add -net 161.26.0.0 netmask 255.255.0.0 gw 10.18.44.1
         bridge_ports eth0
         bridge_stp off
         bridge_fd 0
         bridge_maxwait 0

 # br1 setup with static wan IPv4 with ISP router as a default gateway
 auto br1
 iface br1 inet static
         address 208.43.222.51
         netmask 255.255.255.248
         broadcast 208.43.222.55
         gateway 208.43.222.49
         bridge_ports eth1
         bridge_stp off
         bridge_fd 0
         bridge_maxwait 0

sudo systemctl restart networking
sudo brctl show

minikube start

