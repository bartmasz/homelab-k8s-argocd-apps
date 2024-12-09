# JupyterHub

## ArgoCD Application

```bash
k apply -f application.yml
```

## Local Helm deployment

```bash
helm repo add jupyterhub https://hub.jupyter.org/helm-chart/

helm repo update

helm upgrade --cleanup-on-fail \
  --install myjupyterhub jupyterhub/jupyterhub \
  --namespace jupyterhub \
  --create-namespace \
  --version=4.0.0 \
  --values config.yaml
```

```md
       __                          __                  __  __          __
      / / __  __  ____    __  __  / /_  ___    _____  / / / / __  __  / /_
 __  / / / / / / / __ \  / / / / / __/ / _ \  / ___/ / /_/ / / / / / / __ \
/ /_/ / / /_/ / / /_/ / / /_/ / / /_  /  __/ / /    / __  / / /_/ / / /_/ /
\____/  \__,_/ / .___/  \__, /  \__/  \___/ /_/    /_/ /_/  \__,_/ /_.___/
              /_/      /____/

       You have successfully installed the official JupyterHub Helm chart!

### Installation info

  - Kubernetes namespace: jupyterhub
  - Helm release name:    myjupyterhub
  - Helm chart version:   4.0.0
  - JupyterHub version:   5.2.1
  - Hub pod packages:     See https://github.com/jupyterhub/zero-to-jupyterhub-k8s/blob/4.0.0/images/hub/requirements.txt

### Followup links

  - Documentation:  https://z2jh.jupyter.org
  - Help forum:     https://discourse.jupyter.org
  - Social chat:    https://gitter.im/jupyterhub/jupyterhub
  - Issue tracking: https://github.com/jupyterhub/zero-to-jupyterhub-k8s/issues

### Post-installation checklist

  - Verify that created Pods enter a Running state:

      kubectl --namespace=jupyterhub get pod

    If a pod is stuck with a Pending or ContainerCreating status, diagnose with:

      kubectl --namespace=jupyterhub describe pod <name of pod>

    If a pod keeps restarting, diagnose with:

      kubectl --namespace=jupyterhub logs --previous <name of pod>

  - Verify an external IP is provided for the k8s Service proxy-public.

      kubectl --namespace=jupyterhub get service proxy-public

    If the external ip remains <pending>, diagnose with:

      kubectl --namespace=jupyterhub describe service proxy-public

  - Verify web based access:

    You have not configured a k8s Ingress resource so you need to access the k8s
    Service proxy-public directly.

    If your computer is outside the k8s cluster, you can port-forward traffic to
    the k8s Service proxy-public with kubectl to access it from your
    computer.

      kubectl --namespace=jupyterhub port-forward service/proxy-public 8080:http

    Try insecure HTTP access: http://localhost:8080
```
