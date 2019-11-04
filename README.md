# GitOps 101

```sh

git clone https://github.com/mhausenblas/gitops101.git 

kubectl apply -f ./flux/

# download  fluxctl from https://github.com/fluxcd/flux/releases/tag/1.15.0
# for example, for Linux:
# curl -L -o fluxctl https://github.com/fluxcd/flux/releases/download/1.15.0/fluxctl_linux_amd64
chmod +x fluxctl

./fluxctl identity
# configure GitHub with above public key

# edit flux/flux-deployment.yaml:
# --git-url=<GIT URL OF YOUR REPOSITORY>
# --git-path=deploy/kubernetes

kubectl apply -f flux/flux-deployment.yaml

cp examples/podinfo-dep.yaml deploy/kubernetes
git add deploy
git commit -m "adds new deployment to cluster"
git push origin master

# wait for some 5min until you see the podinfo deployment and pod:
watch kubectl get pods,deploy
```