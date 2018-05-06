# Terraform DigitalOcean Knit

> Knit terraform and ansible together using /var/lib/cloud/instance/boot-finished

## Usage example

```
ssh-keygen -q -b 2048 -t rsa -N '' -f id_rsa
export TF_VAR_do_token="$(lpass show --notes do_token)"
terraform init
terraform plan
terraform apply -auto-approve
ansible-playbook playbook.yml
ip=$(terraform state show digitalocean_droplet.web | awk '/ipv4_address/ { print $NF }')
ssh -i id_rsa appuser@$ip echo hello world
terraform destroy -force
```