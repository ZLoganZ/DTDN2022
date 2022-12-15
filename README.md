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
###
Trước hết ta dùng lệnh
```
$ sudo su
# sudo apt-get update -y
```
Thực hiện lệnh cài đặt:
```
# sudo apt-get install -y docker.io
```
Kiểm tra phiên bản docker bằng lệnh
```
# docker version
```
Bước 2: Cài đặt kubeclt
###
Download về phiên bản kubeclt mới nhất với lệnh
```
# curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl
```
Cài đặt kubeclt với lệnh sau:
```
# chmod +x ./kubectl
# sudo mv ./kubectl /usr/local/bin/kubectl
```
Kiểm tra cài đặt bằng lệnh:
```
# kubectl version --client
```
Bước 3: Cài đặt Conntrack với lệnh sau
```
# sudo apt install conntrack
```
Bước 4: Cài đặt minikube
###
Download file cài đặt và cấp quyền thực thi bằng lệnh
```
# curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
# chmod +x minikube
```
Tiến hành cài đặt minikube
```
# sudo mv minikube /usr/local/bin/
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
```
Kiểm tra các thành phần đang chạy
```
# kubectl get all
```
Truy web với ip máy và port 30000
```
Ex: http://192.168.49.2:30000/
```
