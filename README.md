# K8s Self-Hosted Media Gateway

![Kubernetes](https://img.shields.io/badge/Kubernetes-1.27-blue?style=flat-square&logo=kubernetes)
![Cloudflare Tunnel](https://img.shields.io/badge/Cloudflare%20Tunnel-Enabled-amber?style=flat-square&logo=cloudflare)
![Traefik](https://img.shields.io/badge/Traefik-Reverse%20Proxy-teal?style=flat-square&logo=traefik)
![Jellyfin](https://img.shields.io/badge/Jellyfin-Media%20Server-purple?style=flat-square&logo=jellyfin)
![CI/CD](https://img.shields.io/badge/GitHub%20Actions-CI%2FCD-limegreen?style=flat-square&logo=githubactions)

## 🎬 Overview
**k8s-selfhosted-media-gateway** is a Kubernetes-powered, self-hosted media stack designed for secure remote access, automation, and scalability. This project integrates:

| Component                          | Description                                                               |
|------------------------------------|---------------------------------------------------------------------------|
| 🎥 **Jellyfin & Jellyseerr**       | Media streaming and request management                                    |
| 📦 **ARR Stack**                   | Radarr, Sonarr, Lidarr, Bazarr, Prowlarr for automated media organization |
| 📡 **qBittorrent & SABnzbd**       | Torrent and Usenet downloaders                                            |
| 🔒 **Traefik & Cloudflare Tunnel** | Secure remote access without port forwarding                              |
| 🔑 **Authentik (OAuth)**           | Authentication and user access control                                    |
| 📊 **Prometheus, Grafana, Loki**   | Monitoring and centralized logging                                        |
| ⚙️ **Helm charts**                 | Simplified deployment and upgrades                                        |

---
## 🏗 Features
### 📈 High Availability & Scalability
- Stateful workloads for **Jellyfin & ARR stack**
- **Horizontal Pod Autoscaling (HPA)** for demand-based scaling
- **Persistent Volume Claims (PVCs)** for storage durability

### 🔐 Secure & Remote Access
- **Cloudflare Tunnel** for secure remote access without port forwarding
- **Traefik Reverse Proxy** with automatic SSL via Let's Encrypt
- **OAuth Authentication with Authentik** for access control

### 🎥 Automated Media Management
- **Jellyfin** – Open-source media server
- **Jellyseerr** – Media request & management platform
- **ARR Stack** – Full media automation suite
- **Downloaders** – SABnzbd (Usenet) & qBittorrent (Torrent)

### 📡 Monitoring & Logging
- **Prometheus & Grafana** for real-time system insights
- **Loki & Promtail** for centralized logging
- **Alerting & Metrics visualization**

---
## 📂 Directory Structure
```bash
k8s-selfhosted-media-gateway/
├── clusters/
│   ├── media-cluster/
│   │   ├── media-servers/
│   │   │   ├── jellyfin/
│   │   │   ├── jellyseerr/
│   │   ├── cloudflared/
│   ├── arr-cluster/
│   │   ├── automation/
│   ├── download-cluster/
│   │   ├── vpn/
│   │   ├── downloaders/
│   ├── proxy-cluster/
│   │   ├── traefik/
│   │   ├── authentik/
│   │   ├── flaresolverr/
│   ├── monitoring-cluster/
│   ├── maintenance-cluster/
│   ├── helm/
```
---
## 🚀 Deployment Guide
### 📋 Prerequisites
- A **Kubernetes cluster** (K3s, EKS, or Minikube)
- **kubectl** and **Helm** installed
- **Cloudflare Tunnel credentials**

### 📥 Clone the Repository
```bash
git clone https://github.com/stephenjacobsio/k8s-selfhosted-media-gateway.git
cd k8s-selfhosted-media-gateway
```

### 🔧 Configure Secrets & Configurations
#### Set Up Cloudflare Tunnel
```bash
kubectl create secret generic cloudflared-credentials \
  --from-file=clusters/media-cluster/cloudflared/secret.yaml \
  -n media
```
#### Set Up OAuth (Authentik)
Modify `clusters/proxy-cluster/authentik/configmap.yaml` with your Authentik details.

### ▶️ Deploy the Stack
```bash
kubectl apply -f clusters/
```
For Helm-based deployment:
```bash
helm install media-gateway helm/
```

### 🔍 Verify Services
Check pod status:
```bash
kubectl get pods -A
```
Check running services:
```bash
kubectl get svc -A
```

---
## 🌍 Accessing Services
| Service        | URL                                 |
|----------------|-------------------------------------|
| **Jellyfin**   | `https://jellyfin.yourdomain.com`   |
| **Jellyseerr** | `https://jellyseerr.yourdomain.com` |
| **Grafana**    | `https://grafana.yourdomain.com`    |
| **Authentik**  | `https://auth.yourdomain.com`       |

---
## 🔄 Updating the Stack
To apply new configurations or upgrades:
```bash
kubectl apply -f clusters/
```
For Helm users:
```bash
helm upgrade media-gateway helm/
```

---
## 🎯 Roadmap & Future Enhancements
- [ ] Add CI/CD pipeline for automated deployments
- [ ] Enable PostgreSQL backend for ARR stack
- [ ] Implement custom Grafana dashboards
- [ ] Support GeoIP-based access restrictions

---
## 🤝 Contributing
1. Fork the repository
2. Create a feature branch: `git checkout -b feature-name`
3. Commit changes: `git commit -m "Added feature XYZ"`
4. Push to GitHub: `git push origin feature-name`
5. Open a Pull Request

---
## ⚖️ License
This project is licensed under the **MIT License**. See [LICENSE](LICENSE) for details.

---
<p align="center">
  <a href="https://stephenjacobs.io">
    <img src="https://img.shields.io/badge/Made%20with%20❤️%20by-Stephen%20Jacobs-blue?style=for-the-badge" alt="Made with ❤️ by Stephen Jacobs">
  </a>
</p>

