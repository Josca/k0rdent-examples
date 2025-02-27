# Deploy Open WebUI

~~~bash
# Install open-webui service template to k0rdent
helm upgrade --install open-webui oci://ghcr.io/k0rdent/catalog/charts/kgst -n kcm-system \
  --set "helm.repository.url=https://helm.openwebui.com" \
  --set "helm.charts[0].name=open-webui" \
  --set "helm.charts[0].version=5.20.0"

# Create clusterdeployment with unique name
sed "s/SUFFIX/${USER}/g" 01-open-webui/cld.yaml | kubectl apply -f -

# Deploy service using multiclusterservice
kubectl apply -f 01-open-webui/mcs-aws.yaml
~~~
