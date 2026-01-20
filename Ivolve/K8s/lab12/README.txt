Lab 12: Managing Configuration and Sensitive Data
1. Objective
Separate environment configuration from sensitive credentials using Kubernetes ConfigMaps and Secrets.

2. Implementation Using CLI Dry-Run
Step 1: Create ConfigMap for Non-Sensitive Data
We store the database host and user using the following command:
kubectl create configmap mysql-config \
  --from-literal=DB_HOST=mysql-service \
  --from-literal=DB_USER=ivolve_user \
  --dry-run=client -o yaml > mysql-configmap.yaml

kubectl apply -f mysql-configmap.yaml
Step 2: Create Secret for Sensitive Data
For the secret, we ensure the data is encoded. Although kubectl handles encoding with --from-literal, we verify the values:
kubectl create secret generic mysql-credentials \
  --from-literal=DB_PASSWORD=dbpass \
  --from-literal=MYSQL_ROOT_PASSWORD=rootpass \
  --dry-run=client -o yaml > mysql-secret.yaml

kubectl apply -f mysql-secret.yaml
Step 3: Verify the Resources
Check that both resources exist in the cluster:
kubectl get configmap mysql-config
kubectl get secret mysql-credentials
3. Configuration Mapping
KeyStorage TypeValue (Plain)DB_HOSTConfigMapmysql-serviceDB_USERConfigMapivolve_userDB_PASSWORDSecretdbpassMYSQL_ROOT_PASSWORDSecretrootpass
