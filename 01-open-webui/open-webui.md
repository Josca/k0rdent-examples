# Deploy Open WebUI

~~~bash
# Install open-webui service template to k0rdent
helm upgrade --install open-webui oci://ghcr.io/k0rdent/catalog/charts/kgst -n kcm-system \
  --set "helm.repository.url=https://helm.openwebui.com" \
  --set "helm.charts[0].name=open-webui" \
  --set "helm.charts[0].version=5.14.0"

# Deploy aws managed cluster
kubectl apply -f 02-open-webui/clusterdeployment.yaml

# Deploy multicluster service
kubectl apply -f 02-open-webui/mcs-openwebui.yaml

# export managed cluster kubeconfig
kubectl get secret aws-example-kubeconfig -o=jsonpath={.data.value} | base64 -d > kubeconfigs/aws-example
# set managed cluster context
export KUBECONFIG=kubeconfigs/aws-example
kubectl get pods -A
# unset manged cluster context
unset KUBECONFIG
~~~
