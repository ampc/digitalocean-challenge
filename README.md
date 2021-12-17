# digitalocean-challenge
Repo for 2021 Kubernetes Challenge by DigitalOcean. 

## Requirements
- Create a [DigitalOcean Kubernetes Cluster](https://cloud.digitalocean.com/kubernetes/clusters/new)
- Create a [DigitalOcean Container Registry](https://cloud.digitalocean.com/registry)
- Install [kubectl](https://kubernetes.io/docs/tasks/tools/#kubectl)
- Install [doctl](https://github.com/digitalocean/doctl#installing-doctl)
- Install [helm](https://helm.sh/docs/intro/install/)


## Integrate Registry with the cluster
![Integrate Registry with cluster](img/integrate-registry.png)

## Connect to the cluster
- Get cluster kubeconfig using the appropriate command
    - Example: `$ doctl kubernetes cluster kubeconfig save <REDACTED>`
- Check cluster access
    ```bash
    $ kubectl cluster-info
    
    Kubernetes control plane is running at https://<REDACTED>.k8s.ondigitalocean.com
    CoreDNS is running at https://<REDACTED>.k8s.ondigitalocean.com/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy

    To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.
    ```
## Install Kyverno
- Add Kyverno Helm repository and scan for new charts
    - `$ helm repo add kyverno https://kyverno.github.io/kyverno/`
    - `$ helm repo update`

- Install Kyverno chart in the cluster
    - `$ helm install kyverno kyverno/kyverno --namespace kyverno --create-namespace`
    ![Kyverno chart install](img/kyverno-install.png)

- Check if Kyverno pod is running
    ```
    $ kubectl get pods
    NAME                       READY   STATUS    RESTARTS   AGE
    kyverno-6d94754db4-nbbvq   1/1     Running   0          3m20s
    ```