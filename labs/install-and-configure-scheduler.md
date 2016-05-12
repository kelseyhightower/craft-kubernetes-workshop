# Install and configure the Kubernetes Scheduler

## node0

```
gcloud compute ssh node0
```

### Create the kube-scheduler systemd unit file:

```
sudo sh -c 'echo "[Unit]
Description=Kubernetes Scheduler
Documentation=https://github.com/GoogleCloudPlatform/kubernetes

[Service]
ExecStart=/usr/local/bin/hyperkube \
  scheduler \
  --master=http://127.0.0.1:8080
Restart=on-failure
RestartSec=5

[Install]
WantedBy=multi-user.target" > /etc/systemd/system/kube-scheduler.service'
```

Start the kube-scheduler service:

```
sudo systemctl daemon-reload
sudo systemctl enable kube-scheduler
sudo systemctl start kube-scheduler
```

### Verify

```
sudo systemctl status kube-scheduler
kubectl get cs
```
