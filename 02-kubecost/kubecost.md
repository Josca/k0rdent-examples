# Deploy Open WebUI

~~~bash
# Install open-webui service template to k0rdent
helm upgrade --install kubecost oci://ghcr.io/k0rdent/catalog/charts/kgst -n kcm-system \
  --set "helm.repository.url=https://kubecost.github.io/cost-analyzer/" \
  --set "prefix=kubecost-" \
  --set "helm.charts[0].name=cost-analyzer" \
  --set "helm.charts[0].version=2.5.3"
~~~
