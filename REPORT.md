# BÁO CÁO THỰC HÀNH: KIỂM TRA CÀI ĐẶT DOCKER ENGINE VÀ CHẠY CONTAINER HELLO-WORLD

- **Bài thực hành:** Bài 1 - Session 09
- **Mục tiêu:** Thực hành chạy các lệnh kiểm tra phiên bản Docker CLI, Docker Daemon và khởi chạy container đầu tiên trên máy cá nhân.
- **Đường dẫn nộp bài:** `homework/session_09/ex1/REPORT.md`

---

## 1. Kiểm tra phiên bản Docker (`docker version`)

Lệnh thực hiện:
```bash
docker version
```

### Kết quả đầu ra (Terminal Output)
```text
Client: Docker Engine - Community
 Version:           27.3.1
 API version:       1.47
 Go version:        go1.22.7
 Git commit:        ce12230
 Built:             Fri Sep 20 11:41:00 2024
 OS/Arch:           linux/amd64
 Context:           default

Server: Docker Engine - Community
 Engine:
  Version:          27.3.1
  API version:      1.47 (minimum version 1.24)
  Go version:       go1.22.7
  Git commit:       4123429
  Built:            Fri Sep 20 11:41:00 2024
  OS/Arch:          linux/amd64
  Experimental:     false
 containerd:
  Version:          v1.7.22
  GitCommit:        7f7fdf5cedd04996ab7a10ac07c41a4a6012c8b8
 runc:
  Version:          1.1.14
  GitCommit:        v1.1.14-0-g2c9f560
 docker-init:
  Version:          0.19.0
  GitCommit:        de40ad0
```

> **Ghi chú:** Kết quả hiển thị đầy đủ thông tin của cả Client và Server (Docker Daemon) mà không cần dùng tiền tố `sudo`, chứng tỏ user hiện tại đã có quyền truy cập vào Docker Daemon.

---

## 2. Kiểm tra thông tin hệ thống Docker (`docker info`)

Lệnh thực hiện:
```bash
docker info
```

### Kết quả đầu ra (Terminal Output)
```text
Client: Docker Engine - Community
 Version:    27.3.1
 Context:    default
 Debug Mode: false
 Plugins:
  buildx: Docker Buildx (Docker Inc.)
    Version:  v0.17.1
    Path:     /usr/libexec/docker/cli-plugins/docker-buildx
  compose: Docker Compose (Docker Inc.)
    Version:  v2.29.7
    Path:     /usr/libexec/docker/cli-plugins/docker-compose

Server:
 Containers: 0
  Running: 0
  Paused: 0
  Stopped: 0
 Images: 0
 Server Version: 27.3.1
 Storage Driver: overlay2
  Backing Filesystem: extfs
  Supports d_type: true
  Using metacopy: false
 Logging Driver: json-file
 Cgroup Driver: systemd
 Cgroup Version: 2
 Plugins:
  Volume: local
  Network: bridge host ipvlan macvlan null overlay
  Log: awslogs fluentd gcplogs gelf journald json-file local splunk syslog
 Swarm: inactive
 Runtimes: io.containerd.runc.v2 runc
 Default Runtime: runc
 Init Binary: docker-init
 containerd version: 7f7fdf5cedd04996ab7a10ac07c41a4a6012c8b8
 runc version: v1.1.14-0-g2c9f560
 init version: de40ad0
 Security Options:
  apparmor
  seccomp
   Profile: builtin
  cgroupns
 Kernel Version: 6.8.0-45-generic
 Operating System: Ubuntu 24.04.1 LTS
 OSType: linux
 Architecture: x86_64
 CPUs: 4
 Total Memory: 7.648GiB
 Name: devops-node
 ID: 7fc7c6a9-8588-46fb-a0b2-e1c79cbe8784
 Docker Root Dir: /var/lib/docker
 Debug Mode: false
 Experimental: false
 Insecure Registries:
  127.0.0.0/8
 Live Restore Enabled: false
```

> **Ghi chú:** Lệnh `docker info` trả về các thông số chi tiết của Docker Engine bao gồm phiên bản OS, Storage Driver (`overlay2`), Cgroup Driver (`systemd`), số lượng container, image hiện có và cấu hình bảo mật.

---

## 3. Khởi chạy Container đầu tiên (`docker run hello-world`)

Lệnh thực hiện:
```bash
docker run hello-world
```

### Kết quả đầu ra (Terminal Output)
```text
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
c1ec31eb5944: Pull complete 
Digest: sha256:305243c734571da2d100c8c8b3c3140e61142246e639c87901244ac9a6c4c986
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```

---

## 4. Đánh giá & Kết luận

1. **Kết quả kiểm tra:**
   - Xuất hiện đầy đủ thông điệp mong đợi: 
     > `Hello from Docker! This message shows that your installation appears to be working correctly.`
   - Docker CLI kết nối thông suốt với Docker Daemon qua Socket mà không cần sử dụng quyền `sudo`.
   - Quá trình tải image từ Docker Hub và khởi tạo container thực thi thành công.

2. **Xử lý phân quyền (nếu gặp lỗi permission denied):**
   - Đã đảm bảo user hiện tại thuộc group `docker`:
     ```bash
     sudo usermod -aG docker $USER && newgrp docker
     ```
