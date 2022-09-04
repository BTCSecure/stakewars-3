## 1. Download and install Grafana OSS

- Get latest release Grafana OSS from [https://grafana.com/grafana/download?platform=linux](https://grafana.com/grafana/download?platform=linux)

```
wget https://dl.grafana.com/oss/release/grafana_9.0.5_amd64.deb
sudo dpkg -i grafana_9.0.5_amd64.deb
```

- Start the grafana-server

To start the service and verify that the service has started:

```
sudo systemctl daemon-reload
sudo systemctl start grafana-server
sudo systemctl status grafana-server
```

## 2. Download and install Prometheus and Node Exporter

- Create a user for Prometheus and Node Exporter

***Note:***
**Prometheus** - is simply a database with values for metrics. Quite often, Prometheus is configured in conjunction with Grafana, which allows you to visualize metrics.
**Node Exporter** - is necessary for collecting Linux system indicators, such as CPU load, monitoring file systems, disks, network statistics (and others).

```
sudo useradd --no-create-home --shell /usr/sbin/nologin prometheus
sudo useradd --no-create-home --shell /bin/false node_exporter
```

- Create folders
    
    ```
    sudo mkdir /etc/prometheus
    sudo mkdir /var/lib/prometheus
    ```
    

- Set the ownership of these directories
    
    ```
    sudo chown prometheus:prometheus /etc/prometheus
    sudo chown prometheus:prometheus /var/lib/prometheus
    ```
    

- Download the latest version of **Node Exporter** [https://prometheus.io/download/](https://prometheus.io/download/):
    
    ```
    wget https://github.com/prometheus/node_exporter/releases/download/<LATEST VERSION>/node_exporter-<LATEST VERSION>linux-amd64.tar.gz
    
    tar xvf node_exporter-<LATEST VERSION>linux-amd64.tar.gz
    
    sudo cp node_exporter-<LATEST VERSION>linux-amd64/node_exporter /usr/local/bin
    sudo chown node_exporter:node_exporter /usr/local/bin/node_exporter
    ```
    

- Create the Systemd service file node_exporter

```
sudo nano /etc/systemd/system/node_exporter.service
```

```
[Unit]
Description=Node Exporter
Wants=network-online.target
After=network-online.target

[Service]
User=node_exporter
Group=node_exporter
Type=simple
ExecStart=/usr/local/bin/node_exporter

[Install]
WantedBy=multi-user.target
```

```
sudo systemctl daemon-reload
sudo systemctl start node_exporter
sudo systemctl status node_exporter
```

- Download the latest version of **Prometheus** [https://prometheus.io/download/](https://prometheus.io/download/):
    
    ```
    wget https://github.com/prometheus/prometheus/releases/download/<LATEST VERSION>/prometheus-<LATEST VERSION>linux-amd64.tar.gz
    
    tar xfz prometheus-<LATEST VERSION>linux-amd64.tar.gz
    cd prometheus-<LATEST VERSION>linux-amd64/
    
    sudo cp ./prometheus /usr/local/bin/
    sudo cp ./promtool /usr/local/bin/
    
    sudo chown prometheus:prometheus /usr/local/bin/prometheus
    sudo chown prometheus:prometheus /usr/local/bin/promtool
    
    sudo cp -r ./consoles /etc/prometheus
    sudo cp -r ./console_libraries /etc/prometheus
    
    sudo chown -R prometheus:prometheus /etc/prometheus/consoles
    sudo chown -R prometheus:prometheus /etc/prometheus/console_libraries
    ```
    

- Configure **Prometheus**
    
    ```
    sudo nano /etc/prometheus/prometheus.yml
    ```
    
    ```
    global:
      scrape_interval:     15s
      evaluation_interval: 15s
    
    rule_files:
      # - "first.rules"
      # - "second.rules"
    
    scrape_configs:
      - job_name: 'near_node'
        scrape_interval: 5s
        static_configs:
          - targets: ['localhost:9090'] # example - targets: ['99.999.99.99:3030']
    ```
    
    ```
    sudo chown prometheus:prometheus /etc/prometheus/prometheus.yml
    ```
    

- Create the Systemd service file prometheus
    
    ```
    sudo nano /etc/systemd/system/prometheus.service
    ```
    
    ```
    [Unit]
    Description=Prometheus Monitoring
    Wants=network-online.target
    After=network-online.target
    
    [Service]
    User=prometheus
    Group=prometheus
    Type=simple
    ExecStart=/usr/local/bin/prometheus \
    --config.file /etc/prometheus/prometheus.yml \
    --storage.tsdb.path /var/lib/prometheus/ \
    --web.console.templates=/etc/prometheus/consoles \
    --web.console.libraries=/etc/prometheus/console_libraries
    ExecReload=/bin/kill -HUP $MAINPID
    
    [Install]
    WantedBy=multi-user.target
    ```
    
    ```
    sudo systemctl daemon-reload
    sudo systemctl start prometheus
    sudo systemctl status prometheus
    ```
    

## 3. Sign in to Grafana

To sign in to Grafana for the first time:

- Open your web browser and go to `http://<IP>:3000/`. The default HTTP port that Grafana listens to is 3000 unless you have configured a different port.
- On the sign-in page, enter admin for the username and password.
- Click Sign in.

If successful, you will see a prompt to change the password.

- Click OK on the prompt and change your password.

***Note:*** We strongly recommend that you change the default administrator password. We recommend no less than 14 characters including numbers, symbols, uppercase, and lowercase letters.

- Create a **new view-only user**

Log in under admin and go to:

- Server Admin – Users
- Click “New user”
- Fill out he fields and Click “Create user”
- Configuration – Users. Check “Role” in the newly created user. There should be “Viewer” permissions.

***Note:*** Create a strong password. We recommend no less than 14 characters including numbers, symbols, uppercase, and lowercase letters.

- Create **Data Sources / Prometheus**
- Click the configuration gear icon, then Data Source
- Select prometheus
- Set URL to [http://localhost:9090](http://localhost:9090/)
- Click **Save & Test**

If everything is fine, then you will see a message.

- Add **Dashboard**

## Link to our grafana:

[http://65.109.22.107:3000/d/rYdddlPWkgg/near?orgId=1&refresh=30s&from=now-24h&to=now](http://65.109.22.107:3000/d/rYdddlPWkgg/near?orgId=1&refresh=30s&from=now-24h&to=now)

**Login: Guest**

**Password: 123**

### Software dashboard screen:

![ch18-software-1.png](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-018/ch18-software-1.png)

### Hardware dashboard screen:

![ch18-hardware-1.png](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-018/ch18-hardware-1.png)
***
⏪[Challenge 014](https://github.com/BTCSecure/stakewars-3/blob/main/challenge-014.md)     | [Оглавление](https://github.com/BTCSecure/stakewars-3)⏩
:---|---:
