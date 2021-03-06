---
title: Manual Trigger | Guides
description: Manual Trigger
menu:
  docs_0.1.0:
    identifier: guides-trigger
    name: Manual Trigger
    parent: guides-basics
    weight: 2
menu_name: docs_0.1.0
section_menu_id: guides
---

> New to KubeCI engine? Please start [here](/docs/0.1.0/concepts/README).

# Manual Trigger

This tutorial will show you how to trigger a Workflow manually. There are two possible triggering scenarios:

- `workflow.spec.triggers` empty: You can trigger such workflows only using manual trigger. For that you should leave `trigger.spec.request` empty.
- `workflow.spec.triggers` not empty: Your `trigger.spec.request` object must satisfy one of `workflow.spec.triggers`. You can also leave `trigger.spec.request` empty, but `envFromPath` will set to empty in that case.

Here, we will use the same workflow used in previous [hello-world](hello_world.md) example, but trigger it without creating any ConfigMap. Note that, for force trigger we have to set `allowManualTrigger` to true.

Before we start, you need to have a Kubernetes cluster, and the kubectl command-line tool must be configured to communicate with your cluster. If you do not already have a cluster, you can create one by using [Minikube](https://github.com/kubernetes/minikube). Now, install KubeCI engine in your cluster following the steps [here](/docs/0.1.0/setup/engine/install).

To keep things isolated, we are going to use a separate namespace called `demo` throughout this tutorial.

```console
$ kubectl create ns demo
namespace/demo created
```

## Configure RBAC

You need to specify a service-account in `spec.serviceAccount` to ensure RBAC for the workflow. This service-account along with operator's service-account must have `list` and `watch` permissions for the resources specified in `spec.triggers`.

First, create a service-account for the workflow. Then, create a cluster-role with ConfigMap `list` and `watch` permissions. Now, bind it with service-accounts of both workflow and operator.

```console
$ kubectl apply -f ./docs/examples/engine/manual-trigger/rbac.yaml
serviceaccount/wf-sa created
clusterrole.rbac.authorization.k8s.io/wf-role created
rolebinding.rbac.authorization.k8s.io/wf-role-binding created
clusterrolebinding.rbac.authorization.k8s.io/operator-role-binding created
```

## Create Workflow

```console
$ kubectl apply -f ./docs/examples/engine/manual-trigger/workflow.yaml
workflow.engine.kube.ci/sample-workflow created
```

```yaml
apiVersion: engine.kube.ci/v1alpha1
kind: Workflow
metadata:
  name: sample-workflow
  namespace: demo
spec:
  serviceAccount: default
  executionOrder: Serial
  allowManualTrigger: true
  steps:
  - name: step-hello
    image: alpine
    commands:
    - echo
    args:
    - hello world
```

## Trigger Workflow

Now trigger the workflow by creating a `Trigger` custom-resource which contains a complete ConfigMap resource inside `.request` section.

```console
$ kubectl apply -f ./docs/examples/engine/manual-trigger/trigger.yaml
trigger.extensions.kube.ci/sample-trigger created
```

```yaml
apiVersion: extensions.kube.ci/v1alpha1
kind: Trigger
metadata:
  name: sample-trigger
  namespace: demo
workflows:
- sample-workflow
request:
  apiVersion: v1
  kind: ConfigMap
  metadata:
    name: sample-config
    namespace: demo
  data:
    example.property.1: hello
    example.property.2: world
```

Whenever a workflow is triggered, a workplan is created and respective pods are scheduled.

```console
$ kubectl get workplan -l workflow=sample-workflow -n demo
NAME                    CREATED AT
sample-workflow-nv4jn   13s
```

```console
$ kubectl get pods -l workplan=sample-workflow-nv4jn -n demo
NAME                      READY   STATUS      RESTARTS   AGE
sample-workflow-nv4jn-0   0/1     Completed   0          29s
```

## Trigger without request

You can also trigger the workflow by omitting `trigger.spec.request`.

```console
$ kubectl apply -f ./docs/examples/engine/manual-trigger/trigger-without-request.yaml
trigger.extensions.kube.ci/sample-trigger created
```

```yaml
apiVersion: extensions.kube.ci/v1alpha1
kind: Trigger
metadata:
  name: sample-trigger
  namespace: demo
workflows:
- sample-workflow
```

## Trigger using KubeCI CLI

You can also use KubeCI CLI to trigger workflows. In order to use KubeCI CLI as `kubectl` plugin follow the steps [here](/docs/0.1.0/setup/cli/install).

**Without request:**

```console
$ kubectl ci trigger sample-workflow -n demo
trigger.extensions.kube.ci/sample-workflow-trigger created
```

**With request:**

You can specify request using `--by` flag.

```yaml
$ kubectl ci trigger sample-workflow -n demo --by "$(cat docs/examples/engine/manual-trigger/configmap.yaml)" -o yaml

apiVersion: extensions.kube.ci/v1alpha1
kind: Trigger
metadata:
  creationTimestamp: null
  name: sample-workflow-trigger
  namespace: demo
  selfLink: /apis/extensions.kube.ci/v1alpha1/namespaces/demo/triggers/sample-workflow-trigger
request:
  apiVersion: v1
  data:
    example.property.1: hello
    example.property.2: world
  kind: ConfigMap
  metadata:
    name: sample-config
    namespace: demo
workflows:
- sample-workflow
```

## Cleanup

```console
$ kubectl delete ns demo
namespace "demo" deleted
```
