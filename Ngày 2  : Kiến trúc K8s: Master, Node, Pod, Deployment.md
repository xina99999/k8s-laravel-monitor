

---

## ✅ **Ngày 2 – Task: Kiến trúc K8s: Master, Node, Pod, Deployment**

---

### 🎯 **Mục tiêu cuối ngày**

* Hiểu rõ thành phần Master và Node trong K8s
* Nắm được khái niệm Pod, Deployment, ReplicaSet
* Biết vai trò của API Server, Controller, Scheduler, v.v.
* Vẽ sơ đồ kiến trúc K8s và mô hình triển khai app cơ bản

---

## 🧠 1. Tổng quan kiến trúc Kubernetes

Kubernetes là hệ thống **orchestrator container**, gồm 2 nhóm thành phần chính:

### 🧩 1.1 **Control Plane (Master Node)**

| Thành phần                 | Vai trò                                   |
| -------------------------- | ----------------------------------------- |
| `kube-apiserver`           | Gateway giao tiếp giữa user và cluster    |
| `etcd`                     | Lưu trữ cấu hình và trạng thái cluster    |
| `kube-scheduler`           | Gán Pod vào Node phù hợp                  |
| `kube-controller-manager`  | Theo dõi trạng thái & tự động hóa hành vi |
| `cloud-controller-manager` | Quản lý tài nguyên cloud (nếu có)         |

---

### 🏗️ 1.2 **Worker Node**

| Thành phần          | Vai trò                                            |
| ------------------- | -------------------------------------------------- |
| `kubelet`           | Quản lý Pod trong Node, nhận lệnh từ Control Plane |
| `kube-proxy`        | Quản lý routing và network                         |
| `container runtime` | Docker, containerd – nơi chạy container thực tế    |

---

## 📦 2. Các đối tượng cơ bản trong K8s

| Đối tượng      | Vai trò                                                               |
| -------------- | --------------------------------------------------------------------- |
| **Pod**        | Đơn vị nhỏ nhất, chứa 1 hoặc nhiều container                          |
| **Deployment** | Quản lý lifecycle Pod: update, scale, rollback                        |
| **ReplicaSet** | Đảm bảo số lượng Pod luôn đúng                                        |
| **Service**    | Cung cấp địa chỉ truy cập tới Pod (ClusterIP, NodePort, LoadBalancer) |

---

## 📊 3. Vẽ sơ đồ kiến trúc Kubernetes

Bạn có thể vẽ tay hoặc dùng công cụ sau:

* [https://excalidraw.com/](https://excalidraw.com/)
* [https://draw.io/](https://draw.io/)
* [https://app.diagrams.net/](https://app.diagrams.net/)

### ✅ Sơ đồ gợi ý cần bao gồm:

```
+----------------------+
|     Control Plane    |
|----------------------|
| API Server           |
| Scheduler            |
| Controller Manager   |
| etcd (Database)      |
+----------+-----------+
           |
           | (kubectl / CI/CD tool)
           v
+--------------------------+         +--------------------------+
|      Worker Node 1       |         |      Worker Node 2       |
|--------------------------|         |--------------------------|
| kubelet + kube-proxy     |         | kubelet + kube-proxy     |
| Pod: Laravel App         |         | Pod: MySQL               |
| Pod: Redis               |         | Pod: Node Exporter       |
+--------------------------+         +--------------------------+

                <------ Cluster Network ------->
```

👉 Bạn nên vẽ kèm:

* 1 Control Plane (master)
* 2 Worker Nodes
* Mỗi Node có 1–2 Pod chạy container app như Laravel, MySQL, Redis...

---

## 📝 4. Task thực hành

### Bước 1: Đọc & ghi chú kiến trúc K8s

* Ghi chép vai trò của các thành phần trong file `day2-notes.md`

### Bước 2: Vẽ sơ đồ kiến trúc K8s

* Dùng Excalidraw, Draw\.io hoặc vẽ tay chụp ảnh

### Bước 3: Viết mô tả hoạt động thực tế

Ví dụ:

> "Khi mình dùng `kubectl apply -f deploy.yaml`, lệnh này đi đến `API Server`, API Server lưu lại vào `etcd`, sau đó `Scheduler` chọn 1 node để tạo Pod, `kubelet` nhận nhiệm vụ chạy container đó."

---

### ✅ Kết quả kỳ vọng

| Task                                                   | Trạng thái |
| ------------------------------------------------------ | ---------- |
| Hiểu kiến trúc Control Plane & Worker Node             | ✅          |
| Biết vai trò các thành phần: kubelet, API Server, v.v. | ✅          |
| Vẽ sơ đồ kiến trúc cluster (có Pod, Service)           | ✅          |
| Mô tả dòng xử lý `kubectl apply` → Pod chạy            | ✅          |

---
