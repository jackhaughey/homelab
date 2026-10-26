# Homelab Infrastructure

Infrastructure-as-Code repository for my personal Kubernetes homelab.

This project serves as a platform for learning and practising modern infrastructure engineering, automation, containerisation, and Kubernetes administration using industry-standard tools and workflows.

## Objectives

- Build a repeatable Kubernetes environment from bare Linux hosts
- Use Infrastructure as Code wherever possible
- Develop practical experience with Ansible automation
- Gain hands-on understanding of Kubernetes components and cluster operations
- Experiment with Git-based workflows and infrastructure version control

## Technologies

- Red Hat Enterprise Linux
- Ansible
- Kubernetes
- Kubeadm
- Containerd
- Git & GitHub

## Lab Topology

```text
┌─────────────────┐
│ rhel-admin-01   │
│ Ansible Control │
└────────┬────────┘
         │
         ▼

┌─────────────────────┐
│ k8s-control-01      │
│ Kubernetes Control  │
│ Plane Node          │
└─────────┬───────────┘
          │
 ┌────────┴────────┐
 ▼                 ▼

┌─────────────┐  ┌─────────────┐
│ k8s-worker- │  │ k8s-worker- │
│ 01          │  │ 02          │
└─────────────┘  └─────────────┘
```

## Repository Structure

```text
homelab/
├── ansible/
│   ├── inventory.yml
│   ├── group_vars/
│   ├── playbooks/
│   └── docs/
└── README.md
```

## Ansible Playbooks

Current playbooks automate:

- Kubernetes node prerequisites
- Repository configuration
- Swap disablement
- Kernel module configuration
- Sysctl configuration
- Containerd installation and configuration
- Systemd cgroup configuration
- kubelet installation
- Cluster validation checks

## Deployment Workflow

The environment is built incrementally using Ansible:

1. Configure repositories
2. Install Kubernetes prerequisites
3. Configure kernel modules and sysctl settings
4. Disable swap
5. Install and configure containerd
6. Enable systemd cgroups
7. Install kubelet, kubeadm and kubectl
8. Validate node readiness
9. Initialise the cluster with kubeadm

## Validation

Examples of validation performed after deployment include:
```
ansible kubernetes -i inventory.yml -a "swapon --show"
ansible kubernetes -i inventory.yml -a "sysctl net.ipv4.ip_forward"
ansible kubernetes -i inventory.yml -a "systemctl status containerd"
```

## Learning Goals

This repository documents my journey into:

  -  Platform Engineering
  -  Site Reliability Engineering (SRE)
  -  Kubernetes Administration
  -  Infrastructure Automation
  -  Linux Systems Engineering

## Future Enhancements

  -  Cluster bootstrap automation
  -  CNI deployment
  -  GitOps with ArgoCD
  -  Monitoring with Prometheus and Grafana
  -  Certificate management
  -  Storage provisioning
  -  CI/CD validation pipelines

## Disclaimer
This is a personal homelab project used for learning, experimentation, and skills development. It is not intended to represent a production-ready deployment.
