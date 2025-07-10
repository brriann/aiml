# kubeflow


## Installation steps

1. install golang

https://go.dev/doc/install

2. install kind

https://kind.sigs.k8s.io/

3. install kubeflow

https://www.kubeflow.org/docs/started/installing-kubeflow/

- clone kubeflow manifests repo (to ~/dev/kubeflow_manifests)

https://github.com/kubeflow/manifests

- create kind cluster

```bash
cat <<EOF | kind create cluster --name=kubeflow --config=-
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
- role: control-plane
  image: kindest/node:v1.32.0@sha256:c48c62eac5da28cdadcf560d1d8616cfa6783b58f0d94cf63ad1bf49600cb027
  kubeadmConfigPatches:
  - |
    kind: ClusterConfiguration
    apiServer:
      extraArgs:
        "service-account-issuer": "https://kubernetes.default.svc"
        "service-account-signing-key-file": "/etc/kubernetes/pki/sa.key"
EOF
```

- create k8s secret

```bash
docker login

kubectl create secret generic regcred \
    --from-file=.dockerconfigjson=$HOME/.docker/config.json \
    --type=kubernetes.io/dockerconfigjson
```

- install kubeflow using kustomize (kubectl -c)

```bash
cd ~/dev/kubeflow_manifests
while ! kubectl apply --server-side --force-conflicts -k example; do echo "Retrying to apply resources"; sleep 20; done
```

- fix known kind issue for Pods in broken state with "too many open files" in container logs

https://kind.sigs.k8s.io/docs/user/known-issues/#pod-errors-due-to-too-many-open-files


```bash
docker exec -it kubeflow-control-plane sh
$ sudo sysctl fs.inotify.max_user_watches=524288
$ sudo sysctl fs.inotify.max_user_instances=512
```

## Usage

https://www.kubeflow.org/docs/components/central-dash/overview/

https://www.kubeflow.org/docs/components/katib/user-guides/hp-tuning/configure-experiment/#search-algorithms-in-detail

https://www.kubeflow.org/docs/components/katib/user-guides/early-stopping/
