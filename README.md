# clair

## To install

```
git clone https://github.com/satchpx/clair.git
cd clair/helm
helm dependency update clair
helm install --name clair clair
```

## Troubleshooting

#### If the installation fails, make sure `tiller` service account is created with the appropriate RBAC
```
kubectl create serviceaccount --namespace kube-system tiller
kubectl create clusterrolebinding tiller-cluster-rule --clusterrole=cluster-admin --serviceaccount=kube-system:tiller
kubectl patch deploy --namespace kube-system tiller-deploy -p '{"spec":{"template":{"spec":{"serviceAccount":"tiller"}}}}
kubectl create serviceaccount --namespace default tiller-default
kubectl create clusterrolebinding tiller-cluster-rule --clusterrole=cluster-admin --serviceaccount=kube-system:tiller-default
kubectl patch deploy --namespace default tiller-deploy -p '{"spec":{"template":{"spec":{"serviceAccount":"tiller-deploy"}}}}
```

#### Credits: https://github.com/coreos/clair/blob/master/Documentation/running-clair.md
