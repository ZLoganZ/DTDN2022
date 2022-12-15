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
# kubectl version –short
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
Chạy minikube trên server với lệnh
```
# minikube start --network-plugin=cni --vm-driver=docker --force
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
```
Kiểm tra các thành phần đang chạy
```
# kubectl get all
```
Truy web với ip máy và port 30000
```
Ex: http://192.168.49.2:30000/
```
