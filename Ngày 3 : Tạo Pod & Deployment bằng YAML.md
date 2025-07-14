
---

## ✅ **Ngày 3 – Task: Tạo Pod & Deployment bằng YAML**

---

### 🎯 **Mục tiêu cuối ngày**

* Hiểu sự khác biệt giữa **Pod** và **Deployment**
* Tự viết file YAML để tạo **Pod** và **Deployment**
* Thực thi file YAML với `kubectl apply`
* Kiểm tra, mô tả và xóa tài nguyên đã tạo

---

## 📘 1. Ôn lại lý thuyết ngắn gọn

| Khái niệm      | Mô tả                                           |
| -------------- | ----------------------------------------------- |
| **Pod**        | Đơn vị nhỏ nhất chạy container trong K8s        |
| **Deployment** | Quản lý Pod: scale, update, rollback            |
| **ReplicaSet** | Do Deployment tạo ra, đảm bảo số lượng Pod đúng |

> ❗ **Không nên tạo Pod trực tiếp trong production**, luôn nên dùng Deployment để dễ quản lý.

---

## 🛠️ 2. Viết YAML tạo Pod

### ✏️ `pod-nginx.yaml`

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
  labels:
    app: nginx
spec:
  containers:
    - name: nginx-container
      image: nginx:1.25
      ports:
        - containerPort: 80
```

### ✅ Thực hiện:

```bash
kubectl apply -f pod-nginx.yaml
kubectl get pods
kubectl describe pod nginx-pod
kubectl logs nginx-pod
```

### 🧹 Xóa:

```bash
kubectl delete -f pod-nginx.yaml
```

---

## ⚙️ 3. Viết YAML tạo Deployment

### ✏️ `deployment-nginx.yaml`

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
        - name: nginx
          image: nginx:1.25
          ports:
            - containerPort: 80
```

### ✅ Thực hiện:

```bash
kubectl apply -f deployment-nginx.yaml
kubectl get deployments
kubectl get pods
kubectl describe deployment nginx-deployment
```

---

### 📦 4. Tạo Service để truy cập Pod (bonus)

### ✏️ `service-nginx.yaml`

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  type: NodePort
  selector:
    app: nginx
  ports:
    - port: 80
      targetPort: 80
      nodePort: 30080
```

```bash
kubectl apply -f service-nginx.yaml
minikube service nginx-service
```

---

## 📝 5. Task thực hành chi tiết

| Task                                      | Mục tiêu                           |
| ----------------------------------------- | ---------------------------------- |
| Viết `pod-nginx.yaml`                     | Pod chạy 1 container nginx         |
| Viết `deployment-nginx.yaml`              | Tạo 2 replicas nginx               |
| Viết `service-nginx.yaml`                 | Có thể truy cập app từ trình duyệt |
| Dùng `kubectl` để apply, describe, delete | Thao tác quản trị cơ bản           |
| Ghi log, mô tả và export trạng thái YAML  | Luyện debugging                    |

---

### ✅ Kết quả kỳ vọng

| Mục tiêu                                         | Trạng thái |
| ------------------------------------------------ | ---------- |
| Tạo Pod nginx từ YAML                            | ✅          |
| Tạo Deployment nginx chạy nhiều bản sao          | ✅          |
| Biết cách expose Pod qua Service                 | ✅          |
| Quản lý bằng `kubectl get`, `describe`, `delete` | ✅          |

---


