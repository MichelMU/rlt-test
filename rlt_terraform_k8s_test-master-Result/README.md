# Run  the Terraform codes to deploy a Kubernetes cluster inside of GCP, and make the Kubernetes cluster private using the following commands:
cd rlt_terraform_k8s_test-master-Result/terraform/
terraform init
terraform plan
terraform apply

# Build rlt-test application image and push into GCR
cd rlt_terraform_k8s_test-master-Result/docker_and_helm_charts/application/rlt-test/
docker build -t rlt-test-image . 
docker tag rlt-test-image gcr.io/root-level-test/rlt-test-image
gcloud docker -- push gcr.io/root-level-test/rlt-test-image

# Deploy the helm charts
cd rlt_terraform_k8s_test-master-Result/docker_and_helm_charts/charts/rlt-test
helm install --name rlt-test-m .   #for helm 2x
helm install rlt-test-m .  #for helm 3x
