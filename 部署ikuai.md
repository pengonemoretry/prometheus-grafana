### 1. 更新系统

首先，确保你的系统是最新的：

bash

复制代码

`sudo dnf update -y`

### 2. 安装 Prometheus 2.54.1

1. **下载 Prometheus**：
    
    bash
    
    复制代码
    
    `wget https://github.com/prometheus/prometheus/releases/download/v2.54.1/prometheus-2.54.1.linux-amd64.tar.gz`
    
2. **解压文件**：
    
    bash
    
    复制代码
    
    `tar xvf prometheus-2.54.1.linux-amd64.tar.gz`
    
3. **移动文件到合适的位置**：
    
    bash
    
    复制代码
    
    `sudo mv prometheus-2.54.1.linux-amd64/prometheus /usr/local/bin/ sudo mv prometheus-2.54.1.linux-amd64/promtool /usr/local/bin/`
    
4. **创建配置目录**：
    
    bash
    
    复制代码
    
    `sudo mkdir /etc/prometheus`
    
5. **移动配置文件和示例配置文件**：
    
    bash
    
    复制代码
    
    `sudo mv prometheus-2.54.1.linux-amd64/prometheus.yml /etc/prometheus/`
    
6. **创建 Prometheus 用户**：
    
    bash
    
    复制代码
    
    `sudo useradd --no-create-home --shell /bin/false prometheus`
    
7. **设置权限**：
    
    bash
    
    复制代码
    
    `sudo chown prometheus:prometheus /usr/local/bin/prometheus sudo chown prometheus:prometheus /usr/local/bin/promtool sudo chown prometheus:prometheus /etc/prometheus/prometheus.yml`
    
8. **创建 Prometheus 服务文件**：
    
    bash
    
    复制代码
    
    `sudo nano /etc/systemd/system/prometheus.service`
    
    内容如下：
    
    ini
    
    复制代码
    
    `[Unit] Description=Prometheus Documentation=https://prometheus.io/docs/introduction/overview/ After=network-online.target  [Service] User=prometheus Group=prometheus ExecStart=/usr/local/bin/prometheus --config.file /etc/prometheus/prometheus.yml Restart=always  [Install] WantedBy=multi-user.target`
    
9. **启动 Prometheus 并设置开机自启**：
    
    bash
    
    复制代码
    
    `sudo systemctl daemon-reload sudo systemctl start prometheus sudo systemctl enable prometheus`
    

### 3. 安装 Grafana 11.2.0

1. **下载 Grafana**：
    
    bash
    
    复制代码
    
    `wget https://dl.grafana.com/oss/release/grafana-11.2.0-1.x86_64.rpm`
    
2. **安装 Grafana**：
    
    bash
    
    复制代码
    
    `sudo dnf install grafana-11.2.0-1.x86_64.rpm`
    
3. **启动 Grafana 并设置开机自启**：
    
    bash
    
    复制代码
    
    `sudo systemctl start grafana-server sudo systemctl enable grafana-server`
    

### 4. 访问 Grafana 和 Prometheus

- **Grafana**: 默认情况下，Grafana 运行在 http://localhost:3000。你可以使用默认的用户名和密码 (`admin/admin`) 登录。
- **Prometheus**: 默认情况下，Prometheus 运行在 http://localhost:9090。

按照这些步骤，你就可以在 CentOS 9 上成功安装并配置 Prometheus 和 Grafana。如果有其他问题或需要进一步的帮助，请告诉我！