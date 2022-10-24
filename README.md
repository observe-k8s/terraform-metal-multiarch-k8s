# Observe k8s Kubernetes on Equinix Metal

[Forked from equinix/terraform-metal-multiarch-k8s](https://github.com/equinix/terraform-metal-multiarch-k8s)
where full [instructions](https://github.com/observe-k8s/terraform-metal-multiarch-k8s/blob/main/README.md)
for terraform project are available.

## Instructions

- Login to Equinix Metal console and create a User API Token.
- Set `auth_token` in `terraform.tfvars` to User API Token from Equinix Metal Console.
- Run `terraform init`
- Run `terraform apply`
  - When complete
    - Run `ssh root@<HOST> tail -f /var/log/cloud-init-output.log` until *Cloud-init v. 22.2-0ubuntu1~18.04.3 finished* is seen
    - Run `ssh root@<HOST> kubectl --kubeconfig=/etc/kubernetes/admin.conf get nodes -w` to ensure control-plane and worker nodes are *Ready*

Cluster is now ready to use.

For a service to have a public IP address, set the Kubernetes Service type to `LoadBalancer`.
