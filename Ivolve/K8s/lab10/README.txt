

	Lab 10: Node Isolation Using Taints in Kubernetes
1. Introduction
This lab focuses on Node Isolation. In a production Kubernetes environment, you often need to ensure that certain nodes are reserved for specific workloads or kept empty for administrative purposes. Taints allow a node to "repel" pods unless those pods have a matching Toleration.

2. Objectives
* Identify nodes in a multi-node cluster.
* Apply a NoSchedule taint to a specific node.
* Verify the node configuration via the CLI.

3. Procedure
Step 1: Verify Cluster Nodes
Before applying taints, ensure your cluster has the required minimum of 2 nodes.
Command:
Minikube start –nodes=2
kubectl get nodes

Step 2: Apply the Taint
Target one of your worker nodes to isolate it. We will use the key node, the value worker, and the NoSchedule effect.
Command:
kubectl taint nodes <your-node-name> node=worker:NoSchedule

Step 3: Verify the Isolation
Describe the nodes to confirm that the taint is active in the node's metadata.
Command:
kubectl describe nodes
Verification Checklist:
* Locate the Taints section in the output.
* Confirm it displays: node=worker:NoSchedule

4. Summary of Configuration
The following table summarizes the taint components used in this lab:
ComponentValueDescriptionKeynodeThe identifier for the taint.ValueworkerThe specific value assigned to the key.EffectNoSchedulePrevents new pods from being placed on the node.
