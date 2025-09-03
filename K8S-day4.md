### NOTES ###


Day 4 – ConfigMaps, Secrets & Feature Toggles

ConfigMap → App settings (non-sensitive). Example: URLs, feature flags.

Secret → Sensitive info (passwords, keys, certs). Base64 encoded.

Feature Toggles → Enable/disable features without redeploy.

Banking Example → Toggle “Recurring Payment” on/off via ConfigMap.

👉 Trick:

ConfigMap = what app does

Secret = what app knows

Scenario Qs:

What if ConfigMap changes? → Pod restart OR Reloader sidecar.

Secret vs ConfigMap? → Sensitive vs non-sensitive.

Real issue? → Wrong ConfigMap key → feature didn’t enable in UAT → fixed with redeploy.

🔹 Day 5 – Storage (PV, PVC), StatefulSets, Jobs & CronJobs
PV & PVC

PV = storage resource in cluster.

PVC = Pod’s claim to request PV.

Decouples storage from Pods.

👉 Banking Example:

Client portal DB microservice → PVC bound to PV (EBS volume).

If Pod dies, data persists on PV.

Scenario Qs:

What if PVC stays pending? → No matching PV → create PV or use dynamic provisioning.

How does it help? → Persistent DB for transactions.

StatefulSet

For stateful apps needing stable network ID + storage.

Pods have sticky identity: pod-0, pod-1, …

Works with Headless Service.

👉 Banking Example:

Cassandra cluster for trade history.

Each node keeps data identity across rescheduling.

Scenario Qs:

Why StatefulSet over Deployment? → DB/data apps need stable identity.

How scale? → New Pod joins cluster with predictable hostname.

Jobs & CronJobs

Job = run once until success.

CronJob = run on schedule.

👉 Banking Example:

Job → data migration before release.

CronJob → nightly reconciliation batch @ 2 AM.

Scenario Qs:

What if Job Pod fails? → Restart until completion.

What if CronJob overlaps? → Use concurrencyPolicy: Forbid.

🔹 Day 6 – Probes & Networking
Health Probes

Readiness Probe → Traffic only when app ready.

Liveness Probe → Restart Pod if unhealthy.

Startup Probe → Delay liveness until app boots.

👉 Banking Example:

Readiness → login service waits for DB connection.

Liveness → restart trade settlement service if it hangs.

Startup → JVM-based apps need long startup.

Scenario Qs:

What if readiness fails but liveness passes? → Pod alive, but no traffic sent.

Real incident? → Login failures fixed by readiness probe on DB pool.

Networking

Each Pod = own IP.

Services = stable IP + DNS.

Ingress = external traffic routing.

NetworkPolicy = security rules.

👉 Banking Example:

Ingress routes clientportal.abnamro.com → backend service.

ClusterIP for internal microservice communication.

NetworkPolicy → only auth-service can talk to DB.

Scenario Qs:

ClusterIP vs NodePort vs LoadBalancer?

How Pods discover each other? → DNS service-name.namespace.svc.cluster.local.

Troubleshooting? → curl inside Pod, check DNS, review NetworkPolicy.

🧠 Revision Tricks

ConfigMap = app behavior, Secret = sensitive knowledge.

PV = actual disk, PVC = claim ticket.

Deployment = stateless, StatefulSet = stateful.

Job = one-time, CronJob = schedule.

Readiness = can I take traffic?, Liveness = am I alive?, Startup = am I booted yet?

ClusterIP = internal, NodePort = node-wide, LB = cloud external.


