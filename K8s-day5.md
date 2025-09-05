Cheat Sheet – Service Mesh (Istio Focus)
🔹 Why Service Mesh?

Manages service-to-service communication in microservices.

Adds observability, security, traffic control without changing code.

🔹 Key Features

Traffic Routing: Canary, blue/green.

Security: mTLS between pods.

Observability: Metrics, logs, tracing.

Resilience: Retries, timeouts, circuit breakers.

🔹 How it Works

Sidecar Proxy (Envoy) injected into each Pod.

All service traffic flows via Envoy proxies.

🔹 Example – Client Portal

Payments v1 → Canary test with v2 (10% traffic first).

mTLS ensures encrypted communication.

Tracing shows request path: Login → Payment → Settlement.

🔹 Interview Scenarios

Q: Why did you use Service Mesh in your project?
A: To secure inter-service comms (mTLS), enable canary releases, and get deep observability across 10+ microservices in the Client Portal.

Q: How is it different from API Gateway?
A: API Gateway manages external → cluster traffic, while Service Mesh manages internal pod-to-pod traffic.

📌 Kubernetes Day 8 Cheat Sheet – Networking Deep Dive
🔹 1. Kubernetes DNS & CoreDNS

Each Service gets a DNS entry (service.namespace.svc.cluster.local).

Example: settlement-service.client-portal.svc.cluster.local.

Makes service discovery stable even if Pod IPs change.

👉 Interview Tip: Mention DNS-based discovery avoids hardcoding IPs.

🔹 2. Network Policies

Restrict Ingress/Egress traffic between Pods.

Default = all Pods can talk to all Pods.

YAML selects Pods by labels + defines allowed comms.

👉 Example in Project:

Payment service can only talk to Auth & Settlement, not directly DB.

👉 Interview Tip: Show this reduces lateral attack risk.

🔹 3. Ingress vs API Gateway

Ingress: L7 routing inside K8s, SSL termination.

API Gateway: Adds auth, rate limiting, transformations, analytics.

Often combined → Ingress for internal routing, Gateway for external clients.

👉 Example in Project:

Ingress routes /login → Auth service.

API Gateway enforces JWT auth + throttling for external clients.

🔹 4. Multi-Cluster Networking

Banks run multiple clusters (per region/env).

Need cross-cluster communication.

Approaches: Istio multi-cluster, AWS VPC Peering, PrivateLink.

👉 Example in Project:

EU & Asia clusters sync settlement APIs for low latency + DR.

👉 Interview Tip:

Say you’d design multi-region HA with multiple EKS clusters + peering/service mesh.