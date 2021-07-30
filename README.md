# flux-sops

A Simple one cluster PoC using Sops secret encryption along with the Flux GitOps workflow.

## Motivation
Research on achieving a secure way of managing day-1 and day-2 operations on secret data and gitOps.

## Take it for a spin

1. Install the requirements
    - [kind](https://kind.sigs.k8s.io/)
    - [fluxcd](https://fluxcd.io/docs/installation/)
    - [gpp](https://gnupg.org/)
    - [kubectl](https://kubernetes.io/docs/tasks/tools/)

2. Fork and clone this repo into your machine.

3. Init kind k8s cluster
```shell
$ kind create cluster
```

4. Bootstrap fluxcd bound to your repo:
```shell
$ export GITHUB_TOKEN=<my_pat>
$ flux bootstrap github \            
  --owner=<my_user> \
  --repository=flux-sops \
  --path=clusters/test \
  --personal
```

5. Verify that fluxcd was installed:
```shell
$ kubectl get po -n flux-system
```

6. Test it by adding a new secret or resource to the main branch and flux should provision it to your kind cluster.
