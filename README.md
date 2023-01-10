### Introduction

This is a simple example of configuring a MachineSet in OpenShift using [Server-Side-Apply](https://argo-cd.readthedocs.io/en/stable/user-guide/sync-options/#server-side-apply) in Argo CD. This feature enables us to provide a partial version of the MachineSet that will be merged into the existing one.

### MachineSet Naming

One of the challenges around managing MachineSets with GitOps is that each MachineSet gets a unique name which cannot be predicted in advance. Give this how can we provide a base configuration that can be used across all MachineSets in a fleet of customers?

In this example we will use kustomize to manage this. A base MachineSet exists in the folder `components/apps/machineset/workers/base` which can then be re-used at the cluster level. To handle the unique naming of the machineset we can simply use a kustomize override to patch the correct name into the partial yaml.

This kustomization for patching the name is located under the `clusters/rhpds/apps/machineset/overrides/workers` folder.