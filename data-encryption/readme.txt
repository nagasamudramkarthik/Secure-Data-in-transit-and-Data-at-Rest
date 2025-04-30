vault commands:

helm repo add hashicorp https://helm.releases.hashicorp.com
helm repo update
helm install vault hashicorp/vault   --namespace encrypt   --set server.dev.enabled=true   --set injector.enabled=true
vault server - dev
