# Prior Art and Adjacent Ecosystem References

> **Status: References, NOT adopted canon.**
>
> This document collects public prior art and adjacent ecosystem references for
> infrastructure-as-code. These are listed for orientation, vocabulary, and
> comparison only. Their inclusion here does **not** mean they are adopted
> canon, endorsed, or required by this repository. Nothing in this file
> overrides [`docs/principles.md`](principles.md) or
> [`docs/v0.1-boundary.md`](v0.1-boundary.md). Where a concept below appears in
> this repo's schemas or examples, it is because it was chosen through the
> packet process — not because it appears here.

## Purpose of this document

- Provide a shared vocabulary for discussing infrastructure-as-code.
- Surface adjacent ecosystems that solve related problems.
- Make the boundaries of this repo's scope legible against the wider field.
- Keep prior art visible without canonizing it.

## Public prior art

### Terraform

- **What it does:** A declarative IaC tool that uses HCL to describe cloud and
  on-prem infrastructure, driven by a plan/apply workflow against a persisted
  state file.
- **Relevance to this repo:** Establishes widely-used vocabulary (plan/apply,
  state, providers, modules, backends) that this repo references for
  orientation. This repo does not adopt HCL or HashiCorp-specific semantics.
- **Docs:** https://developer.hashicorp.com/terraform/docs

### Pulumi

- **What it does:** An IaC platform that lets authors define infrastructure in
  general-purpose programming languages (TypeScript, Python, Go, etc.) with a
  state-backed engine.
- **Relevance to this repo:** Illustrates the "infrastructure as real source
  code" posture and the trade-offs between declarative DSLs and
  general-purpose languages. Referenced for comparison only.
- **Docs:** https://www.pulumi.com/docs/

### AWS CloudFormation

- **What it does:** AWS-native declarative IaC service that provisions and
  manages AWS resources from JSON/YAML templates with stack-based lifecycle
  management.
- **Relevance to this repo:** A canonical example of cloud-provider-native
  declarative infrastructure and stack semantics. Referenced as a vocabulary
  anchor for "template" and "stack."
- **Docs:** https://docs.aws.amazon.com/cloudformation/

### Ansible

- **What it does:** An agentless configuration management and automation tool
  driven by YAML playbooks, emphasizing idempotent imperative-ish tasks over
  SSH.
- **Relevance to this repo:** Represents the configuration-management branch
  of the ecosystem and the agentless, idempotent-task model. Referenced to
  distinguish "configuration management" from "infrastructure provisioning."
- **Docs:** https://docs.ansible.com/

### Chef

- **What it does:** A configuration management platform using "cookbooks" and
  "recipes" written in a Ruby DSL, with a client/server model and agent-based
  convergence.
- **Relevance to this repo:** A historical anchor for the
  configuration-management lineage and the "infrastructure as code" phrase.
  Referenced for vocabulary (cookbook, recipe, convergence) only.
- **Docs:** https://docs.chef.io/

### Puppet

- **What it does:** A declarative configuration management system using a
  domain-specific language (Puppet DSL) and a compiled catalog applied by an
  agent to enforce desired state.
- **Relevance to this repo:** Illustrates the desired-state / catalog model
  and the concept of drift from compiled intent. Referenced for comparison
  only.
- **Docs:** https://www.puppet.com/docs

### SaltStack (Salt)

- **What it does:** An event-driven configuration management and remote
  execution platform using "states" and "pillars," with a master/minion
  topology.
- **Relevance to this repo:** Represents the event-driven and remote-execution
  branch of configuration management. Referenced for vocabulary (state,
  pillar, highstate) only.
- **Docs:** https://docs.saltproject.io/

### AWS CDK / Cloud Development Kits

- **What it does:** A framework that lets authors define cloud infrastructure
  in general-purpose languages, which is then synthesized into declarative
  templates (e.g., CloudFormation) for deployment.
- **Relevance to this repo:** Illustrates the "imperative authoring ->
  declarative artifact" pattern and the role of synthesis. Referenced for
  comparison only.
- **Docs:** https://docs.aws.amazon.com/cdk/

## Adjacent ecosystem

### OpenTofu

- **What it does:** An open-source, Linux Foundation–governed fork of
  Terraform that preserves the Terraform-style HCL workflow and provider
  ecosystem under an OSI-approved license.
- **Relevance to this repo:** A relevant open-source alternative in the
  Terraform-compatible space. Referenced for orientation on licensing and
  governance of IaC tooling.
- **Docs:** https://opentofu.org/docs/

### Crossplane

- **What it does:** A Kubernetes-native control plane that lets teams
  provision and manage cloud infrastructure via Kubernetes custom resources,
  treating infrastructure as Kubernetes objects reconciled by controllers.
- **Relevance to this repo:** Illustrates the "infrastructure as Kubernetes
  CRs" and control-plane-as-IaC pattern. Referenced to mark the boundary
  between file-based IaC and API-reconciled control planes.
- **Docs:** https://docs.crossplane.io/

### Cluster API

- **What it does:** A Kubernetes subproject that provides declarative
  lifecycle management of Kubernetes clusters themselves via Kubernetes custom
  resources and providers.
- **Relevance to this repo:** A reference point for declarative
  cluster-lifecycle management and the "infrastructure managing
  infrastructure" pattern. Referenced for comparison only.
- **Docs:** https://cluster-api.sigs.k8s.io/

### Argo CD

- **What it does:** A GitOps continuous delivery tool for Kubernetes that
  reconciles a Git repository's desired state with live clusters.
- **Relevance to this repo:** A primary reference for the GitOps delivery
  pattern and the "Git as source of truth" posture. Referenced for vocabulary
  (reconciliation, sync, desired vs. live state).
- **Docs:** https://argo-cd.readthedocs.io/

### Flux

- **What it does:** A GitOps toolkit for Kubernetes that continuously
  reconciles cluster state from Git, Helm, and other sources via controllers.
- **Relevance to this repo:** A second primary reference for GitOps and
  continuous reconciliation. Referenced alongside Argo CD to show the range of
  GitOps implementations.
- **Docs:** https://fluxcd.io/docs/

## Vocabulary references

These terms appear across the ecosystem and are collected here so that
discussions in this repo have a shared frame. Their presence here is
definitional, not prescriptive.

- **IaC (Infrastructure as Code):** Treating infrastructure provisioning and
  configuration as version-controlled source material. See
  [`docs/definition.md`](definition.md) for this repo's working definition.
- **GitOps:** A pattern where Git is the source of truth and agents reconcile
  live state toward it. References: Argo CD, Flux.
- **Declarative infrastructure:** Describing *what* the desired state is
  rather than the imperative steps to reach it. References: Terraform,
  CloudFormation, Puppet, Crossplane.
- **Drift detection:** Comparing recorded desired state against observed live
  state to surface divergence. References: Terraform (`terraform plan` /
  refresh), Puppet (catalog enforcement), Argo CD / Flux (sync status).

## Key concepts

These concepts recur across the prior art above and are useful when reading
this repo's schemas and examples. They are descriptive of the field, not
adopted as this repo's canon.

- **State files:** A persisted record of what an IaC tool believes it has
  provisioned, used to compute diffs and plan changes. Reference: Terraform
  state.
- **Plan / apply:** A two-phase workflow where a tool first computes a change
  plan for review, then applies it. Reference: Terraform.
- **Modules:** Reusable, composable units of infrastructure definition.
  Reference: Terraform modules, Pulumi components, CloudFormation nested
  stacks.
- **Providers:** Plugins that translate IaC declarations into calls against
  specific cloud or service APIs. Reference: Terraform providers, Pulumi
  providers.
- **Backends:** The storage and coordination mechanism for state (e.g.,
  remote backends, locking). Reference: Terraform backends.

## Note on adoption

This repo deliberately separates **references** from **adopted canon**. Per
[`docs/principles.md`](principles.md):

> Separate examples from adopted operating canon.

Items listed here are references for the field. Only concepts that survive the
packet process and appear in `schemas/`, `examples/`, and audited receipts
count as adopted canon for this repository.
