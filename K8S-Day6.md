Final Kubernetes Cheat Sheet (Day 1–10 Master)

👉 Use this as quick recall before interviews. Short + crisp + keyword style.

🔹 Day 1–2 (Basics)

Pod = Smallest unit

Deployment = Replica mgmt

Service = ClusterIP / NodePort / LoadBalancer

ConfigMap = App settings

Secret = Sensitive data (base64)

Ingress = External routing

🔹 Day 3–4 (Storage & Jobs)

PV/PVC = Storage binding

StorageClass = Dynamic PV

Job = Run once → batch

CronJob = Schedule tasks

Feature Toggle = ConfigMap flags

🔹 Day 5–6 (Probes & Networking)

Liveness Probe = Restart if unhealthy

Readiness Probe = Remove from Service until ready

Startup Probe = Delay checks until start

K8s Networking = CNI, kube-proxy, CoreDNS

Service Mesh = Istio/Linkerd → observability, traffic split

🔹 Day 7–8 (Scaling & Updates)

HPA = Scale Pods

VPA = Adjust Pod resources

Cluster Autoscaler = Scale nodes

RollingUpdate = Gradual rollout

Canary = Small % rollout

Blue/Green = Parallel envs

🔹 Day 9 (Security, Observability)

RBAC = Who can do what

PodSecurity Admission = No privileged/root

ResourceQuota = Namespace limits

Observability = EFK, Prometheus, Grafana, Jaeger

Velero = Backup K8s + PVs

CI/CD = Jenkins + Helm + EKS

🔹 Day 10 (Advanced & Ops)

StatefulSet = Stable ID storage apps

DaemonSet = Runs on all nodes (logging, monitoring)

Init Container = Pre-start tasks

Sidecar = Helper container

Multi-tenancy = Namespace + RBAC + Quotas

CRDs/Operators = Extend Kubernetes

Upgrade = Drain → Nodegroup upgrade

Troubleshoot = Logs → Events → DNS → Resources