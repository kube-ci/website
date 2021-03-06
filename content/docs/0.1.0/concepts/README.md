---
title: KubeCI Concepts
menu:
  docs_0.1.0:
    identifier: concepts-readme
    name: Overview
    parent: concepts
    weight: 10
menu_name: docs_0.1.0
section_menu_id: concepts
url: /docs/0.1.0/concepts/
aliases:
  - /docs/0.1.0/concepts/README/
---

# Concepts

Concepts help you learn about the different parts of the KubeCI and the abstractions it uses.

<ul class="nav nav-tabs" id="conceptsTab" role="tablist">
  <li class="nav-item">
    <a class="nav-link active" id="engine-tab" data-toggle="tab" href="#engine" role="tab" aria-controls="engine" aria-selected="true">KubeCI Engine</a>
  </li>
  <li class="nav-item">
    <a class="nav-link" id="git-apiserver-tab" data-toggle="tab" href="#git-apiserver" role="tab" aria-controls="git-apiserver" aria-selected="false">Git API Server</a>
  </li>
</ul>
<div class="tab-content" id="conceptsTabContent">
  <div class="tab-pane fade show active" id="engine" role="tabpanel" aria-labelledby="engine-tab">

- What is KubeCI engine?
  - [Overview](/docs/0.1.0/concepts/engine/what-is-kubeci-engine/overview). Provides a conceptual introduction to KubeCI engine, including the problems it solves and its high-level architecture.
- Custom Resource Definitions
  - [Workflow](/docs/0.1.0/concepts/engine/crds/workflow). Introduces the concept of `Workflow` for configuring a set of tasks in a Kubernetes native way.
  - [Workflow Template](/docs/0.1.0/concepts/engine/crds/workflow_template). Introduces the concept of `WorkflowTemplate` to invoke a template with arguments for different workflows.
  - [Workplan](/docs/0.1.0/concepts/engine/crds/workplan). Introduces the concept of `Workplan` that represents the final state of a workflow after it is triggered.
  - [Trigger](/docs/0.1.0/concepts/engine/crds/trigger). Introduces the concept of `Trigger` that represents a fake create event for a Kubernetes resource to trigger workflows.
  - [Workplan Log](/docs/0.1.0/concepts/engine/crds/workplan_log). Introduces the concept of `WorkplanLog` that can be used to collect logs of any workplan step.

</div>
<div class="tab-pane fade" id="git-apiserver" role="tabpanel" aria-labelledby="git-apiserver-tab">

- What is Git API server?
  - [Overview](/docs/0.1.0/concepts/git-apiserver/what-is-git-apiserver/overview). Provides a conceptual introduction to Git API server, including the problems it solves and its high-level architecture.
- Custom Resource Definitions
  - [Repository](/docs/0.1.0/concepts/git-apiserver/crds/repository). Introduces the concept of `Repository` for syncing a git repository in a Kubernetes native way.
  - [Branch](/docs/0.1.0/concepts/git-apiserver/crds/branch). Introduces the concept of `Branch` to represent branches of git repositories.
  - [Tag](/docs/0.1.0/concepts/git-apiserver/crds/tag). Introduce concept of `Tag` to represent tags of git repositories.
  - [PullRequest](/docs/0.1.0/concepts/git-apiserver/crds/pull_request). Introduce concept of `PullRequest` to represent pull-requests of remote git repositories.
  - [GithubEvent](/docs/0.1.0/concepts/git-apiserver/crds/github_event). Introduce concept of `GithubEvent` that represents Github events.
  
</div>
