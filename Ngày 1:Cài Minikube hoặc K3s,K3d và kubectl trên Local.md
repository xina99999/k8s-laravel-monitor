
---

## ✅ **Ngày 1 – Task: Cài Minikube hoặc K3s/K3d + kubectl**

---

### 🎯 **Mục tiêu cuối ngày**

* Cài đặt thành công Minikube hoặc K3s/K3d
* Cài `kubectl` và chạy được lệnh `kubectl get nodes`
* Cluster hoạt động, đã sẵn sàng cho việc tạo Pod

---

### 🧰 1. **Chọn nền tảng triển khai local**

| Tên          | Mô tả                                    | Gợi ý dùng                    |
| ------------ | ---------------------------------------- | ----------------------------- |
| **Minikube** | Dễ dùng, hỗ trợ tốt Docker               | ✅ Dành cho học tập            |
| **K3s**      | Nhẹ, tối ưu cho môi trường resource thấp | VPS / Raspberry Pi            |
| **K3d**      | K3s chạy trong Docker                    | Máy cấu hình yếu + muốn nhanh |

👉 **Khuyên dùng Minikube** nếu bạn đang học trên **Ubuntu, WSL hoặc máy Linux/Mac**, dùng Docker làm runtime.

---

### 🛠️ 2. **Cài đặt Minikube + kubectl**

#### ✅ Bước 1: Cài Docker (nếu chưa có)

```bash
sudo apt update
sudo apt install -y docker.io
sudo usermod -aG docker $USER
newgrp docker
```

#### ✅ Bước 2: Cài `kubectl`

```bash
curl -LO "https://dl.k8s.io/release/$(curl -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x kubectl
sudo mv kubectl /usr/local/bin/
kubectl version --client
```

#### ✅ Bước 3: Cài **Minikube**

```bash
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
```

> Kiểm tra:

```bash
minikube version
```

---

### 🚀 3. **Khởi động Minikube cluster**

```bash
minikube start --driver=docker
```

> Nếu không có Docker Desktop mà đang dùng Linux:

```bash
minikube start --driver=none
```

> Kiểm tra:

```bash
kubectl get nodes
```

---

### 📦 4. (Optional) Cài K3s hoặc K3d

#### ✅ Cài K3s (chạy trực tiếp)

```bash
curl -sfL https://get.k3s.io | sh -
sudo kubectl get node
```

#### ✅ Cài K3d (chạy trong Docker)

```bash
curl -s https://raw.githubusercontent.com/k3d-io/k3d/main/install.sh | bash
k3d cluster create mycluster
kubectl get nodes
```

---

### 🧪 5. Kiểm tra Minikube hoạt động

```bash
kubectl cluster-info
kubectl get pods -A
```

---

### 📌 Ghi chú sau khi hoàn thành

* Nếu cài Minikube, bạn có thể bật dashboard:

```bash
minikube dashboard
```

* Nếu lỗi "no nodes available" → kiểm tra Docker đã chạy chưa:

```bash
sudo systemctl status docker
```

---

### ✅ Kết quả kỳ vọng

| Nội dung                             | Trạng thái |
| ------------------------------------ | ---------- |
| Cài `kubectl` thành công             | ✅          |
| Cluster Minikube hoặc K3s chạy được  | ✅          |
| `kubectl get nodes` hiển thị `Ready` | ✅          |
| Sẵn sàng tạo pod/deployment          | ✅          |

---

