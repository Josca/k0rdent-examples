# k0rdent examples

## Requirements
- Mothership Kubernetes cluster with [k0rdent 0.1.0 installed](https://docs.k0rdent.io/v0.1.0/admin-installation/#install-k0rdent).
- AWS account configured for k0rdent ([guide](https://docs.k0rdent.io/v0.1.0/admin-prepare/#aws), steps 1-8)
- `helm` - The Kubernetes package manager (`brew install helm`)
- `yq` - Tool for simple templates (`brew install yq`)

## Environment
Prepare setup script with your env vars (credentials, secrets, passwords)
~~~bash
cp ./scripts/set_envs_template.sh ./scripts/set_envs.sh
chmod 0600 ./scripts/set_envs.sh  # allow access for file owner only
~~~

Fill vars in your `./scripts/set_envs.sh`. Set environment variables using prepared script.
~~~bash
source ./scripts/set_envs.sh
~~~

## Cloud provider credentials
Create AWS credential resources using helm chart:
~~~bash
helm upgrade --install aws-credential oci://ghcr.io/k0rdent/catalog/charts/aws-credential \
  --version 0.0.1 \
  -n kcm-system \
  -f providers/values-aws-credential.yaml
~~~

Set real secrets values from env vars:
~~~bash
kubectl patch secret aws-credential-secret -n kcm-system -p='{"stringData":{"AccessKeyID":"'$AWS_ACCESS_KEY_ID'"}}'
kubectl patch secret aws-credential-secret -n kcm-system -p='{"stringData":{"SecretAccessKey":"'$AWS_SECRET_ACCESS_KEY'"}}'
~~~

## Examples
- [Open WebUI](./01-open-webui/open-webui.md)
