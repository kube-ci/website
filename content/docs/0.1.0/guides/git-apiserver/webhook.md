---
title: Github Webhook | Guides
description: Github Webhook
menu:
  docs_0.1.0:
    identifier: guides-github-webhook
    name: Github Webhook
    parent: guides-repositories
    weight: 1
menu_name: docs_0.1.0
section_menu_id: guides
---

> New to Git API server? Please start [here](/docs/0.1.0/concepts/README).

# Configure Github Webhook

This tutorial will show you how to configure Github webhook to sync pull-request events.

Before we start, you need to have a Kubernetes cluster, and the kubectl command-line tool must be configured to communicate with your cluster. If you do not already have a cluster, you can create one by using [Minikube](https://github.com/kubernetes/minikube). Now, install Git API server in your cluster following the steps [here](/docs/0.1.0/setup/git-apiserver/install).

First, go to `Webhooks` from settings tab of your Github repository. Now, select `Add webhook` to create a new webhook for the repository. Then, set the followings:

- Payload URL: `https://{master-ip}/apis/webhooks.git.kube.ci/v1alpha1/githubevents`
- Content Type: `application/json`
- SSL verification: Disable

Also, select `Pull Requests` from individual events.