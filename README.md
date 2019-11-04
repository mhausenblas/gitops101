# GitOps 101

## Preparation

Make sure you have a GitHub account set up and visit the trainings environment URL 
provided in the slide deck.

First, fork this repo and clone it:

```sh
git clone https://github.com/USERNAME/gitops101.git 
```

## Set up Flux

Install Flux in the Kubernetes cluster:

```sh
cd gitops101

kubectl apply -f ./flux/
```

Download  `fluxctl` from [github.com/fluxcd/flux/releases](https://github.com/fluxcd/flux/releases/tag/1.15.0) 
and make it executable. For example, for Linux:

```sh
curl -L -o fluxctl https://github.com/fluxcd/flux/releases/download/1.15.0/fluxctl_linux_amd64
chmod +x fluxctl
```

Get the Flux operator's public key:

```sh
./fluxctl identity
```

Next, configure your GitHub repo with above public key (under Settings -> Deploy keys).

Now, edit `flux/flux-deployment.yaml` to change/add:

```sh
 --git-url=<GIT URL OF YOUR REPOSITORY>
 --git-path=deploy/kubernetes
```

And make sure changes are reflected:

```sh
kubectl apply -f flux/flux-deployment.yaml
```

## Example flows

Now GitOps away:

```sh
cp examples/podinfo-dep.yaml deploy/kubernetes
git add deploy
git commit -m "adds new deployment to cluster"
git push origin master
```

Wait for some 5min until you see the `podinfo` deployment and pod:

```sh
watch kubectl get pods,deploy
```

Other things to try:

* Manually delete a deployment (`kubectl delete deploy/podinfo`)
* Scale the `podinfo` deployment to 3 replicas
* More via https://github.com/bricef/gitops-tutorial (the tutorial here is a stripped down version of this one)