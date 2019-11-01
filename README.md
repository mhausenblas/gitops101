# GitOps 101

```sh
kubectl apply -f ./flux/

# download  fluxctl from https://github.com/fluxcd/flux/releases/tag/1.15.0

chmod +x fluxctl

./fluxctl identity

kubectl apply -f flux/flux-deployment.yaml

cp examples/podinfo-dep.yaml deploy/kubernetes
git add deploy
git commit -m "adds new deployment to cluster"
git push origin master

```