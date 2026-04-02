# Kubernetes Internal Developer Platform (IDP)

## Overview

This repository contains a production-grade Internal Developer Platform (IDP) built on Kubernetes.  
The purpose of this project is to model how modern platform engineering teams design, operate, secure, and evolve shared Kubernetes infrastructure at scale.

This platform is intentionally:
- Built incrementally using GitOps
- Operated under realistic constraints
- Subjected to failures and chaos
- Observed and improved through incidents and postmortems

This is not a tutorial repository or a demo cluster. It is an opinionated, operational platform designed to develop deep troubleshooting, system design, and SRE-level thinking.

---

## Platform Objectives

The platform is designed to solve the following real-world problems:

- Safely host workloads for multiple teams on a shared Kubernetes cluster
- Provide self-service deployment while maintaining strong governance
- Enforce security and policy without blocking developer velocity
- Enable deep observability for fast and accurate incident response
- Balance performance, reliability, and infrastructure cost
- Validate resilience through controlled failure injection

---

## High-Level Architecture

Git is the single source of truth for all cluster state.  
All changes are applied through GitOps and continuously reconciled.

High-level flow:

1. Platform, policy, and tenant configurations are defined in Git
2. Argo CD reconciles desired state into the cluster
3. Kubernetes enforces scheduling, isolation, and runtime guarantees
4. Observability, security, and policy systems continuously monitor behavior
5. Failures are injected intentionally and resolved using platform signals

---

## Repository Structure

The repository is organized to clearly separate platform concerns from tenant workloads.

.
├── clusters/
│   └── dev/
│       └── bootstrap and Argo CD applications
│
├── platform/
│   ├── ingress/
│   │   └── ingress controllers and traffic routing
│   ├── networking/
│   │   └── CNI configuration and NetworkPolicies
│   ├── observability/
│   │   └── metrics, logs, traces, profiling
│   ├── security/
│   │   └── runtime security and supply-chain controls
│   ├── policies/
│   │   └── admission and governance policies
│   └── autoscaling/
│       └── HPA, VPA, and node autoscaling
│
├── tenants/
│   ├── team-a/
│   ├── team-b/
│   └── team-c/
│
└── docs/
    ├── runbooks/
    └── incidents/

---

## Technology Stack

Core platform:
- Kubernetes
- GitOps using Argo CD
- Helm and Kustomize for configuration management

Networking:
- NGINX Ingress Controller
- eBPF-based CNI for networking and visibility
- NetworkPolicies for traffic isolation

Observability:
- Prometheus for metrics
- Grafana for visualization
- Loki for logs
- Tempo for distributed tracing
- OpenTelemetry for instrumentation
- Continuous profiling for CPU and memory analysis

Multi-tenancy and governance:
- Namespace-based tenancy model
- Hard isolation using quotas and policies
- Admission control for security and standards enforcement
- API Priority and Fairness for control-plane protection

Security and supply chain:
- Image vulnerability scanning
- Signed container images
- Runtime threat detection
- Least-privilege RBAC and Pod Security Standards

Autoscaling and cost:
- Horizontal Pod Autoscaler
- Vertical Pod Autoscaler
- Node autoscaling with bin-packing
- Namespace-level resource and cost attribution

Chaos and resilience:
- Controlled fault injection
- Node, pod, and network-level failures
- Incident-driven improvements

All tools used are open source and widely adopted in production environments.

---

## Design Principles

1. Git is the source of truth  
   No manual changes are made directly to the cluster.

2. Secure by default  
   Unsafe configurations are rejected before they reach runtime.

3. Observability first  
   Any failure that cannot be observed is treated as a platform defect.

4. Multi-tenant safety  
   Teams are isolated while sharing infrastructure efficiently.

5. Failure is intentional  
   Chaos is used to validate assumptions and improve resilience.

---

## Learning and Operation Model

The platform is evolved through the following loop:

1. Define a real operational problem
2. Implement the minimal required platform capability
3. Inject controlled failures
4. Observe system behavior
5. Debug using platform signals
6. Write postmortems and improve design

This approach prioritizes understanding over tool familiarity.

---

## What This Project Is

- A realistic internal developer platform
- A reference for advanced Kubernetes operations
- A portfolio demonstrating platform ownership
- A system designed to be broken and fixed

---

## What This Project Is Not

- A step-by-step tutorial
- A single-tool showcase
- A production SaaS offering
- A “happy-path-only” Kubernetes setup

---

## How to Use This Repository

1. Bootstrap the cluster using the manifests in clusters/dev
2. Deploy platform components incrementally
3. Onboard tenant workloads
4. Apply policies and security controls
5. Inject failures intentionally
6. Observe, debug, and document outcomes

---

## Intended Audience

- Platform Engineers
- Site Reliability Engineers
- Senior DevOps Engineers
- Engineers preparing for Staff or Principal roles

---

## Author Intent

This project exists to develop deep expertise in Kubernetes platform engineering by building, operating, breaking, and fixing a real system.

Every design decision favors clarity, debuggability, and safety over shortcuts.
