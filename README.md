
# 🛡️ Sovereign Infrastructure: Hyper-Converged Home Lab & DevSecOps Environment

Welcome to the documentation repository for my enterprise-grade home server and secure private cloud.

Inspired by the architecture and strict security standards of modern enterprise datacenters, this project bridges the gap between theoretical cybersecurity concepts and hands-on systems engineering. It is designed for high availability, network hardening, zero-trust access, and infrastructure observability.

## 🏗️ Core Architecture & Tech Stack

This environment is built from the ground up to support containerized microservices, secure remote access, and localized AI processing without relying on third-party public clouds.

* **🖥️ Compute & Virtualization:** Bare-metal host running **Proxmox VE**, managing isolated VMs and Linux Containers (LXC).
* **💾 Enterprise Storage:** **TrueNAS SCALE** virtualized with HBA PCIe pass-through. Managing a 12TB ZFS RAID-Z1 pool (Seagate IronWolf) with LZ4 compression and automated S.M.A.R.T. monitoring.
* **🌐 Networking & Perimeter Security:** Hardened **GL.iNet GL-MT6000 (Flint 2)** router enforcing Policy-Based Routing (PBR) over **WireGuard** tunnels.
* **🔐 Zero-Trust Access (ZTNA):** **Tailscale** mesh overlay network configured with an isolated Subnet Router and Exit Node for secure, identity-based remote administration.
* **🐳 Orchestration & Microservices:** Dedicated Docker VM managed via **Portainer**, hosting isolated application stacks (Jellyfin, Immich ML, n8n automation).
* **👁️ Observability:** Full **Prometheus** and **Grafana** stack providing container-level telemetry, host metrics (Node Exporter), and anomaly detection.

## 📂 Project Documentation

Detailed engineering write-ups, architecture diagrams, and problem-solving methodologies are available in the repository files:

* **[📄 Infrastructure.pdf](./Infrastructure.pdf)** — Bare-metal hardware selection, Proxmox deployment, and mitigating physical I/O bottlenecks.
* **[📄 TrueNAS.pdf](./TrueNAS.pdf)** — ZFS storage architecture, data integrity rules, and managing hardware pass-through.
* [**📄 Pipelines Media.pdf**](./Pipelines Media.pdf) — Automated data acquisition workflows, VPS cloud bridging, and localized machine learning.
* **[📄 Observability & Monitoring.pdf](./Observability%2520%26%2520Monitoring.pdf)** — Building the telemetry stack, reverse-engineering JSON models, and PromQL metric tracking.

## 🛠️ Key Engineering Challenges Solved

The true value of this project lies in the troubleshooting and architectural refinement. Key milestones include:

1. **Mitigating Severe IOwait Lockups:** Re-architected the storage data flow by implementing an NVMe SSD staging layer to handle random write operations before sequentially committing them to the mechanical ZFS array.
2. **iGPU Pass-through & Hardware Acceleration:** Successfully mapped Intel/NVIDIA rendering hardware through the Proxmox hypervisor into an isolated Docker container for efficient media transcoding.
3. **VPN MTU Fragmentation:** Identified and resolved packet loss across the WireGuard tunnels by calculating and clamping the Maximum Transmission Unit (MTU) to account for cryptographic overhead.
4. **Cross-Stack Permission Mapping (UID/GID):** Standardized secure file access across disparate container stacks and TrueNAS NFS mounts using strict least-privilege principles.

## 🚀 Future Roadmap

* **Kubernetes (K8s) Cluster:** Currently scaling the Docker environment into a highly available Kubernetes cluster to dive deeper into container orchestration, Helm charts, and cloud-native DevSecOps postures.
* **Automated Incident Response:** Integrating n8n webhooks with Grafana alerts to trigger automated containment scripts upon detecting anomalous network traffic.
