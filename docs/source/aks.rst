Running automated tasks with CronJob in Azure Kubernetes Service
================================================================

.. code-block:: bash

    az aks create \
        --resource-group myResourceGroup \
        --name myAKSCluster \
        --node-count 1 \
        --attach-acr myContainerRegistry \
        --location westeurope

.. code-block:: bash

    az aks install-cli

.. code-block:: bash

    az aks get-credentials --resource-group myResourceGroup --name myAKSCluster

.. code-block:: bash

    $ kubectl get nodes
    NAME                                STATUS   ROLES   AGE     VERSION
    aks-nodepool1-13211777-vmss000000   Ready    agent   4m14s   v1.18.10

.. code-block:: bash

    az aks nodepool update \
        --resource-group myResourceGroup \
        --cluster-name mAKSCluster \
        --name nodepool1 \
        --enable-cluster-autoscaler \
        --max-count 5 \
        --min-count 1

.. code-block:: bash

    az aks nodepool add \
        --resource-group myResourceGroup \
        --cluster-name mAKSCluster \
        --name turbo \
        --node-count 1 \
        --min-count 0 \
        --max-count 1 \
        --enable-cluster-autoscaler \
        --labels hardware=highmem \
        --node-taints turbo=yes:NoSchedule \
        --max-pods 16 \
        --node-vm-size Standard_DS5_v2

.. code-block:: bash

    az aks nodepool add \
        --resource-group myResourceGroup \
        --cluster-name mAKSCluster \
        --name turbo \
        --node-count 1 \
        --min-count 0 \
        --max-count 1 \
        --enable-cluster-autoscaler \
        --max-pods 16 \
        --node-vm-size Standard_DS5_v2

.. code-block:: bash

    az aks nodepool delete \
        --resource-group myResourceGroup \
        --cluster-name mAKSCluster \
        --name turbo

.. code-block:: bash

    $ kubectl get nodes
    NAME                                STATUS   ROLES   AGE   VERSION
    aks-nodepool1-13211777-vmss000000   Ready    agent   76m   v1.18.10
    aks-turbo-13211777-vmss000000       Ready    agent   61s   v1.18.10

.. code-block:: bash

    $ kubectl get nodes
    NAME                                STATUS   ROLES   AGE   VERSION
    aks-nodepool1-13211777-vmss000000   Ready    agent   97m   v1.18.10

.. code-block:: bash

    az aks update \
        --resource-group myResourceGroup \
        --name mAKSCluster \
        --cluster-autoscaler-profile scale-down-delay-after-add=3m scale-down-unneeded-time=3m

.. code-block:: bash

    kubectl create namespace tasks

.. code-block:: bash

    $ kubectl get pods --all
    NAMESPACE     NAME                                  READY   STATUS    RESTARTS   AGE
    kube-system   coredns-748cdb7bf4-8xzdf              1/1     Running   0          117m
    kube-system   coredns-748cdb7bf4-sbgx4              1/1     Running   0          107m
    kube-system   coredns-autoscaler-868b684fd4-wwn5m   1/1     Running   0          116m
    kube-system   kube-proxy-xs74q                      1/1     Running   0          107m
    kube-system   metrics-server-58fdc875d5-f7f9v       1/1     Running   0          117m
    kube-system   tunnelfront-5b895bbf99-zk75k          1/1     Running   0          116m

.. code-block:: bash

    $ make deploy
    $ make run-now
    $ kubectl get pods --namespace dataflow                                                                                     ✔  dataflow Py  klr-aks-test ○  22:03:05
    NAME                                       READY   STATUS      RESTARTS   AGE
    dataflow-register-2021.01.12.22.02-dlcsh   0/1     Completed   0          2m28s

.. code-block:: bash

    $ kubectl describe pod dataflow-register-2021.01.12.22.02-dlcsh --namespace dataflow
    ...
    Events:
      Type    Reason     Age   From               Message
      ----    ------     ----  ----               -------
      Normal  Scheduled  63s   default-scheduler  Successfully assigned dataflow/dataflow-register-2021.01.12.22.02-dlcsh to aks-nodepool1-13211777-vmss000000
      Normal  Pulling    62s   kubelet            Pulling image "klrcontainerregistry.azurecr.io/dataflow:v0.1"
      Normal  Pulled     39s   kubelet            Successfully pulled image "klrcontainerregistry.azurecr.io/dataflow:v0.1"
      Normal  Created    29s   kubelet            Created container dataflow
      Normal  Started    29s   kubelet            Started container dataflow

.. code-block:: bash

    $ make run-now
    $ kubectl get pods --namespace dataflow

    NAME                                       READY   STATUS    RESTARTS   AGE
    dataflow-register-2021.01.12.22.09-wx22k   0/1     Pending   0          2m11s

.. code-block:: bash

    $ kubectl describe pod dataflow-register-2021.01.12.22.09-wx22k --namespace dataflow
    ...
    Events:
      Type     Reason            Age                   From                Message
      ----     ------            ----                  ----                -------
      Normal   TriggeredScaleUp  3m14s                 cluster-autoscaler  pod triggered scale-up: [{aks-turbo-13211777-vmss 0->1 (max: 1)}]
      Warning  FailedScheduling  2m8s (x3 over 3m16s)  default-scheduler   0/1 nodes are available: 1 node(s) didn't match node selector.
      Normal   Scheduled         75s                   default-scheduler   Successfully assigned dataflow/dataflow-register-2021.01.12.22.36-zpldx to aks-turbo-13211777-vmss000002
      Normal   Pulling           73s                   kubelet             Pulling image "klrcontainerregistry.azurecr.io/dataflow:v0.1"
      Normal   Pulled            58s                   kubelet             Successfully pulled image "klrcontainerregistry.azurecr.io/dataflow:v0.1"
      Normal   Created           50s                   kubelet             Created container dataflow
      Normal   Started           49s                   kubelet             Started container dataflow

.. code-block:: bash

    $ kubectl get nodes
    NAME                                STATUS   ROLES   AGE    VERSION
    aks-nodepool1-13211777-vmss000000   Ready    agent   146m   v1.18.10
    aks-turbo-13211777-vmss000002       Ready    agent   2m8s   v1.18.10



Reference
---------

[1] `Authenticate with Azure Container Registry from Azure Kubernetes Service <https://docs.microsoft.com/en-gb/azure/aks/cluster-container-registry-integration>`__
