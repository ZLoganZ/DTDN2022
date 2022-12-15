# Đề tài: Tìm hiểu về Kubernetes và demo ứng dụng

### Họ tên sinh viên
###
Nguyễn Hoàng Hải `20161051`
###
Nguyễn Văn Đạt `20110455`
###
Tăng Phúc Toàn `20110100`
###
## Các bước cài đặt demo đơn giản
Bước 1: Cài đặt docker
Thực hiện lệnh cài đặt:
```
$ sudo su 
# sudo apt-get update
# sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common
# curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
# sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
# sudo apt-get update
# sudo apt-get install docker-ce docker-ce-cli containerd.io
```
Kiểm tra phiên bản docker bằng lệnh
```
# docker version
```
Bước 2: Cài đặt kubeclt
Download về phiên bản kubeclt mới nhất với lệnh
```
# curl -LO https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl
```
Cài đặt kubeclt với lệnh sau:
```
# sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
```
Kiểm tra cài đặt bằng lệnh:
```
# kubectl version --client
```
Bước 3: Cài đặt Conntrack với lệnh sau
```
# sudo apt-get install -y conntrack
```
Bước 4: Cài đặt minikube
Download file cài đặt và cấp quyền thực thi bằng lệnh
```
# curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
# chmod +x minikube
```
Tiến hành cài đặt minikube
```
# sudo mkdir -p /usr/local/bin/
# sudo install minikube /usr/local/bin/
```
Cài Cri-dockerd
```
# git clone https://github.com/Mirantis/cri-dockerd.git
# wget https://storage.googleapis.com/golang/getgo/installer_linux
# chmod +x ./installer_linux
# ./installer_linux
# source ~/.bash_profile
# cd cri-dockerd
# mkdir bin
# go build -o bin/cri-dockerd
# mkdir -p /usr/local/bin
# install -o root -g root -m 0755 bin/cri-dockerd /usr/local/bin/cri-dockerd
# cp -a packaging/systemd/* /etc/systemd/system
# sed -i -e 's,/usr/bin/cri-dockerd,/usr/local/bin/cri-dockerd,' /etc/systemd/system/cri-docker.service
# systemctl daemon-reload
# systemctl enable cri-docker.service
# systemctl enable --now cri-docker.socket
```
Cài CRI-O Container Runtime
```
# sudo apt update && sudo apt upgrade
# sudo systemctl reboot
# OS=xUbuntu_18.04
# CRIO_VERSION=1.23
# echo "deb https://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable/$OS/ /"|sudo tee /etc/apt/sources.list.d/devel:kubic:libcontainers:stable.list
# echo "deb http://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable:/cri-o:/$CRIO_VERSION/$OS/ /"|sudo tee /etc/apt/sources.list.d/devel:kubic:libcontainers:stable:cri-o:$CRIO_VERSION.list
# curl -L https://download.opensuse.org/repositories/devel:kubic:libcontainers:stable:cri-o:$CRIO_VERSION/$OS/Release.key | sudo apt-key add -
# curl -L https://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable/$OS/Release.key | sudo apt-key add -
# sudo apt update
# sudo apt install cri-o cri-o-runc
# sudo systemctl enable crio.service
# sudo systemctl start crio.service
# sudo apt install cri-tools
```
Sau khi cài tất cả xong thì ta chạy minikube trên server với lệnh
```
# minikube start --vm-driver=none
```
Kiểm tra cài đặt bằng lệnh
```
# minikube status
```
hoặc
```
# kubectl get pods -A
```
Kiểm tra thông tin kubenertes cluster
```
# kubectl cluster-info
```
Kiểm tra các node trong cluster
```
# kubectl get nodes -A
```
Cài Calico CNI
```
# apt install firewalld
# firewall-cmd --add-port=179/tcp --permanent
# firewall-cmd --reload
# curl https://docs.projectcalico.org/manifests/calico.yaml -O
# ls -l calico.yaml
# kubectl apply -f calico.yaml
```
Bước 5: Triển khai mongodb
```
# git clone https://github.com/ZLoganZ/DTDN2022.git
# cd DTDN2022/
# cd mongo/
# kubectl apply -f mongodb-secret.yaml
# kubectl apply -f mongodb-deployment.yaml 
# kubectl apply -f mongo-configmap.yaml
# kubectl apply -f mongo-express-deployment.yaml
# kubectl apply -f mongo-pv.yaml
# kubectl apply -f mongo-roles.yaml
```
Kiểm tra các thành phần đang chạy
```
# kubectl get all
```
Truy web với ip máy và port 30000
```
Ex: http://192.168.49.2:30000/
```
