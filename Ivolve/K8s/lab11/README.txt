Lab 11: Namespace Management and Resource Quota Enforcement
1. Overview
In this lab, we demonstrate how to manage cluster resources by isolating them into a specific Namespace and enforcing a ResourceQuota. This prevents any single namespace from consuming more than its fair share of cluster resources.

2. Lab Objectives
* Create a new namespace named ivolve.
* Generate a ResourceQuota manifest using the kubectl dry-run feature.
* Enforce a limit of 2 pods within the namespace.
* Verify the quota status.

3. Step-by-Step Execution
Step 1: Create the Namespace
Create the logical boundary for our resources:
kubectl create namespace ivolve
Step 2: Generate the Quota Manifest
Instead of writing the YAML from scratch, we use the dry-run command to generate a clean manifest file:
kubectl create quota pod-quota \
  --namespace=ivolve \
  --hard=pods=2 \
  --dry-run=client -o yaml > quota.yaml
Step 3: Apply the Resource Quota
Apply the generated file to the cluster:
kubectl apply -f quota.yaml

