
---

## 🧱 **Task: Cài Minikube hoặc K3s/K3d và kubectl trên Local**

### ✅ Mục tiêu:

* Cài `kubectl` – công cụ dòng lệnh để tương tác với Kubernetes
* Chọn **Minikube** hoặc **K3s/K3d** để tạo môi trường Kubernetes local
* Xác nhận cụm hoạt động và chạy thử pod

---

## 📌 Phần 1: Cài `kubectl`

> `kubectl` là công cụ điều khiển Kubernetes, dùng chung cho cả Minikube và K3s/K3d.

### Bước 1: Cài đặt `kubectl`

```bash
sudo apt update && sudo apt install -y curl apt-transport-https
curl -LO "https://dl.k8s.io/release/$(curl -Ls https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x kubectl
sudo mv kubectl /usr/local/bin/
```

### Bước 2: Kiểm tra phiên bản

```bash
kubectl version --client
```

---

## 📦 **Phần 2A: Cài đặt với Minikube (ưu tiên học tập)**

### Bước 1: Cài Minikube

```bash
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
```

### Bước 2: Cài Docker (nếu chưa có)

```bash
sudo apt update
sudo apt install -y docker.io
sudo usermod -aG docker $USER
newgrp docker
```

### Bước 3: Khởi tạo cluster Minikube

```bash
minikube start --driver=docker
```

### Bước 4: Kiểm tra cluster

```bash
kubectl get nodes
```

---

## 🚀 **Phần 2B: (Tùy chọn)** Cài K3s hoặc K3d

---

### 🥦 Nếu chọn **K3s** (siêu nhẹ, 1 node)

### Bước 1: Cài đặt

```bash
curl -sfL https://get.k3s.io | sh -
```

### Bước 2: Kiểm tra cluster

```bash
sudo kubectl get nodes
```

> Lưu ý: với K3s thì `kubectl` sẽ nằm ở `/usr/local/bin/kubectl` và config tại `/etc/rancher/k3s/k3s.yaml`

---

### 🐳 Nếu chọn **K3d** (chạy K3s trong Docker)

### Bước 1: Cài K3d

```bash
curl -s https://raw.githubusercontent.com/k3d-io/k3d/main/install.sh | bash
```

### Bước 2: Tạo cluster

```bash
k3d cluster create mycluster
```

### Bước 3: Kiểm tra cluster

```bash
kubectl get nodes
```

---

## 🧪 Phần 3: Kiểm tra cụm Kubernetes hoạt động

### Tạo một Pod đơn giản:

```bash
kubectl run nginx --image=nginx --port=80
kubectl get pods
```

### Truy cập pod:

```bash
kubectl expose pod nginx --type=NodePort --port=80
minikube service nginx  # (nếu dùng Minikube)
```

---

## 📝 Ghi chú:

| Tool     | Ưu điểm                       | Nhược điểm               |
| -------- | ----------------------------- | ------------------------ |
| Minikube | Dễ dùng, hỗ trợ GUI dashboard | Nặng hơn, khởi động chậm |
| K3s      | Nhẹ, gần với production       | Cấu hình root nhiều hơn  |
| K3d      | Chạy bằng Docker, linh hoạt   | Yêu cầu Docker chạy tốt  |

---

