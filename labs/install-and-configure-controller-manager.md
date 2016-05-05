# Install and configure the Kubernetes Controller Manager

## node0

```
gcloud compute ssh node0
```

### Create the kube-controller-manager systemd unit file:

```
sudo sh -c 'echo "[Unit]
Description=Kubernetes Controller Manager
Documentation=https://github.com/GoogleCloudPlatform/kubernetes

[Service]
ExecStart=/usr/local/bin/hyperkube \
  controller-manager \
  --master=http://127.0.0.1:8080
Restart=on-failure
RestartSec=5

[Install]
WantedBy=multi-user.target" > /etc/systemd/system/kube-controller-manager.service'
```

Start the kube-controller-manager service:

```
sudo systemctl daemon-reload
sudo systemctl enable kube-controller-manager
sudo systemctl start kube-controller-manager
```

### Verify

```
sudo systemctl status kube-controller-manager
kubectl get cs
```
