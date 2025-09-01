📌 Kubernetes Study Cheat Sheet (Today’s Session)
✅ 1. Horizontal Pod Autoscaler (HPA) & Node Scaling

HPA: Scales pods based on CPU/Memory utilization.

If pods are stuck in Pending state → usually due to insufficient node resources.

Solution:

Increase node instance type (vertical scaling).

Increase node count (horizontal scaling).

For automation → use Cluster Autoscaler (integrates with cloud provider to add/remove nodes automatically when pods are unschedulable).

📌 Scenario (ABN AMRO Client Portal Project)
During peak trading hours, CPU utilization spikes. HPA scaled pods from 1 → 10, but half were Pending. Cluster Autoscaler provisioned new EC2 nodes automatically so pods could be scheduled. This ensured zero downtime and smooth portal access for clients.

✅ 2. Kubernetes Jobs & CronJobs (Batch Processing)

Job: Runs a pod until completion (useful for tasks like DB migrations, data processing).

CronJob: Runs Jobs on a schedule (like Linux cron).

Batch Processing Meaning: Execution of tasks in bulk (e.g., settlement calculations, report generation, end-of-day processes).

In financial/banking systems → batches = scheduled jobs for settlements, reconciliation, compliance reports.

📌 Scenario (ABN AMRO Client Portal Project)
Every night, a CronJob runs settlement batches that reconcile trades executed during the day. If a job fails, DevOps engineers check pod logs (kubectl logs job/<job-name>) and rerun the job. Ensures timely reporting to regulators.

✅ 3. Interview-Ready Scenario-Based Q&A

Q: Pods are in Pending state after HPA triggered scaling. What’s your approach?
A: First check kubectl describe pod to identify reason (usually insufficient resources). If nodes are exhausted, either manually scale node group (eksctl scale nodegroup) or rely on Cluster Autoscaler for automatic scaling. In ABN project, we configured autoscaler to add nodes during peak trading hours, then scale back down to save cost.

Q: Your project uses “batch jobs.” What does that mean in Kubernetes?
A: Batch jobs = scheduled workloads that execute at fixed intervals, e.g., trade settlements or compliance reporting. In our client portal project, we used CronJobs in Kubernetes to automate daily reconciliation tasks. These jobs run independently of user-facing services but are critical for business operations.

✅ End of Day Summary

Learned how HPA + Cluster Autoscaler work together for scaling pods/nodes.

Understood Batch Processing (Jobs/CronJobs) in real-world banking systems.

Practiced scenario-based interview answers tied to ABN AMRO Clearing Bank project.