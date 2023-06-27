### Prometheus Basic Configuration

## Root folder
```
/etc/prometheus/
```
### installation 

```
dnf install wget git net-tools


useradd -m -s /bin/false prometheus


```

# Repo installation

```
sudo vi /etc/yum.repos.d/prometheus-rpm_release.repo

```
```
[prometheus-rpm_release]

name=prometheus-rpm_release

baseurl=https://packagecloud.io/prometheus-rpm/release/el/8/$basearch

repo_gpgcheck=0

gpgcheck=0

enabled=1

gpgkey=https://packagecloud.io/prometheus-rpm/release/gpgkey

sslverify=1

sslcacert=/etc/pki/tls/certs/ca-bundle.crt

metadata_expire=300

[prometheus-rpm_release-source]

name=prometheus-rpm_release-source

baseurl=https://packagecloud.io/prometheus-rpm/release/el/8/SRPMS

repo_gpgcheck=0

gpgcheck=0

enabled=1

gpgkey=https://packagecloud.io/prometheus-rpm/release/gpgkey

sslverify=1

sslcacert=/etc/pki/tls/certs/ca-bundle.crt

metadata_expire=300
```

# Prometheus
```
vi /etc/systemd/system/prometheus.service
```
```
[Unit]

Description=Prometheus Time Series Collection and Processing Server

Wants=network-online.target

After=network-online.target

[Service]

User=prometheus

Group=prometheus

Type=simple

ExecStart=/usr/bin/prometheus \
  --config.file /etc/prometheus/prometheus.yml \
  --storage.tsdb.path /var/lib/prometheus/ \
  --web.console.templates=/etc/prometheus/consoles \
  --web.console.libraries=/etc/prometheus/console_libraries

[Install]

WantedBy=multi-user.target
```

# Start Prometheus
```
systemctl daemon-reload

systemctl start prometheus

systemctl status prometheus
```

# Node Exporter installation
```
sudo dnf install node_exporter

sudo systemctl start node_exporter
```