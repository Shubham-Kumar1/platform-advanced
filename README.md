# Kubernetes Internal Developer Platform (IDP)

## Overview

This repository contains a production-grade Internal Developer Platform (IDP) built on Kubernetes.

The purpose of this project is to model how modern platform engineering teams design, operate, secure, and evolve shared Kubernetes infrastructure at scale.

This platform is intentionally:

* Built incrementally using GitOps
* Operated under realistic constraints
* Subjected to failures and chaos
* Observed and improved through incidents and postmortems

This is **not** a tutorial repository or a demo cluster. It is an opinionated, operational platform designed to develop deep troubleshooting, system design, and SRE-level thinking.

---

## Platform Objectives

The platform is designed to solve real-world problems:

* Safely host workloads for multiple teams on a shared Kubernetes cluster
* Provide self-service deployment while maintaining governance
* Enforce security and policy without blocking developer velocity
* Enable deep observability for fast incident response
* Balance performance, reliability, and infrastructure cost
* Validate resilience through controlled failure injection

---

## High-Level Architecture

Git is the single source of truth for all cluster state.

All changes are applied through GitOps and continuously reconciled.

### Flow

1. Platform, policy, and tenant configurations are defined in Git
2. Argo CD reconciles desired state into the cluster
3. Kubernetes enforces scheduling, isolation, and runtime guarantees
4. Observability, security, and policy systems monitor behavior
5. Failures are injected and resolved using platform signals

---

## Repository Structure

```text
.
├── clusters/
│   └── dev/
│       └── bootstrap-and-argocd-applications/
│
├── platform/
│   ├── ingress/
│   │   └── ingress-controllers-and-traffic-routing/
│   ├── networking/
│   │   └── cni-config-and-network-policies/
│   ├── observability/
│   │   └── metrics-logs-traces-profiling/
│   ├── security/
│   │   └── runtime-security-and-supply-chain/
│   ├── policies/
│   │   └── admission-and-governance/
│   └── autoscaling/
│       └── hpa-vpa-node-autoscaling/
│
├── tenants/
│   ├── team-a/
│   ├── team-b/
│   └── team-c/
│
└── docs/
    ├── runbooks/
    └── incidents/
```

### Structure Principles

* **clusters/** → Cluster bootstrapping and GitOps entrypoint
* **platform/** → Shared infrastructure components
* **tenants/** → Team-owned workloads
* **docs/** → Operational knowledge (runbooks + incidents)

---

## Technology Stack

### Core Platform

* Kubernetes
* Argo CD (GitOps)
* Helm + Kustomize

### Networking

* NGINX Ingress Controller
* eBPF-based CNI
* NetworkPolicies

### Observability

* Prometheus (metrics)
* Grafana (visualization)
* Loki (logs)
* Tempo (tracing)
* OpenTelemetry (instrumentation)
* Continuous profiling

### Multi-Tenancy & Governance

* Namespace-based tenancy
* Resource quotas and limits
* Admission controllers
* API Priority and Fairness

### Security & Supply Chain

* Image vulnerability scanning
* Signed container images
* Runtime threat detection
* Least-privilege RBAC
* Pod Security Standards

### Autoscaling & Cost

* Horizontal Pod Autoscaler (HPA)
* Vertical Pod Autoscaler (VPA)
* Node autoscaling
* Resource attribution per namespace

### Chaos & Resilience

* Fault injection
* Node, pod, and network failures
* Incident-driven improvements

---

## Design Principles

1. **Git is the source of truth**
   No manual changes in the cluster

2. **Secure by default**
   Unsafe configs are rejected early

3. **Observability first**
   Unobservable systems are broken systems

4. **Multi-tenant safety**
   Isolation with efficient sharing

5. **Failure is intentional**
   Chaos validates assumptions

---

## Learning & Operation Model

This platform evolves through an iterative loop:

1. Define a real operational problem
2. Implement minimal capability
3. Inject controlled failures
4. Observe system behavior
5. Debug using signals
6. Write postmortems and improve

This prioritizes **understanding over tooling**.

---

## What This Project Is

* A realistic internal developer platform
* A reference for advanced Kubernetes operations
* A portfolio demonstrating platform ownership
* A system designed to be broken and improved

---

## What This Project Is Not

* A step-by-step tutorial
* A single-tool showcase
* A production SaaS
* A “happy-path-only” setup

---

## Getting Started

1. Bootstrap the cluster using `clusters/dev`
2. Deploy platform components incrementally
3. Onboard tenant workloads
4. Apply policies and security controls
5. Inject failures intentionally
6. Observe, debug, and document

---

## Intended Audience

* Platform Engineers
* Site Reliability Engineers
* Senior DevOps Engineers
* Engineers targeting Staff/Principal roles

---

## Author Intent

This project exists to build deep expertise in Kubernetes platform engineering by:

* Building real systems
* Operating them under constraints
* Breaking them intentionally
* Fixing them through observation and reasoning

Every decision prioritizes:

* Clarity
* Debuggability
* Safety

Over shortcuts.
