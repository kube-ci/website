---
title: Table of Contents | Guides
description: Table of Contents | Guides
menu:
  docs_0.1.0:
    identifier: guides-readme
    name: Readme
    parent: guides
    weight: -1
menu_name: docs_0.1.0
section_menu_id: guides
url: /docs/0.1.0/guides/
aliases:
  - /docs/0.1.0/guides/README/
---

# Guides

Guides show you how to perform tasks with KubeCI engine.

## Workflow Basics

- Learn how to configure and trigger a simple workflow [here](/docs/0.1.0/guides/engine/basics/hello_world).
- Learn how to manually trigger a workflow [here](/docs/0.1.0/guides/engine/basics/manual_trigger).
- Learn how to configure a set of serial tasks [here](/docs/0.1.0/guides/engine/basics/serial_execution).
- Learn how to configure a set of parallel tasks [here](/docs/0.1.0/guides/engine/basics/parallel_execution).
- Learn how to specify DAG dependency [here](/docs/0.1.0/guides/engine/basics/dag_execution).
- Learn how to invoke workflow template [here](/docs/0.1.0/guides/engine/basics/template).
- Learn how shared directories works [here](/docs/0.1.0/guides/engine/basics/shared_directory).
- Learn which environment variables are set by default [here](/docs/0.1.0/guides/engine/basics/implicit_env_var).
- Learn how specify explicit volumes and volume-mounts [here](/docs/0.1.0/guides/engine/basics/volumes).
- Learn how to specify environment variables [here](/docs/0.1.0/guides/engine/basics/env_var).
- Learn how to set environment variables from json-path data [here](/docs/0.1.0/guides/engine/basics/json_path).

## Credential Initializer

- Learn how initialize Docker and Git credentials [here](/docs/0.1.0/guides/engine/credential/credential_initializer).

## CLI and Web UI

- Learn how to use workplan-logs CLI and workplan-viewer web-ui [here](/docs/0.1.0/guides/engine/cli/workplan_status_logs).

## Build and Deploy

- Learn how to build container from source using 
  - [dind](/docs/0.1.0/guides/engine/build/build-dind)
  - [kaniko](/docs/0.1.0/guides/engine/build/build-kaniko)
  - [img](/docs/0.1.0/guides/engine/build/build-img)
- Learn how to deploy your application from source using a single workflow [here](/docs/0.1.0/guides/engine/build/deploy).

## Git Repositories

- Learn how to configure webhook for a Github repository [here](/docs/0.1.0/guides/git-apiserver/webhook).
- Learn how to sync a Github public repository [here](/docs/0.1.0/guides/git-apiserver/github_public).
- Learn how to sync a Github private repository [here](/docs/0.1.0/guides/git-apiserver/github_private).

## Walk-through

- Step by step guide to run go-tests for a Github pull-request and set commit status [here](/docs/0.1.0/guides/walk-through/github_pr).