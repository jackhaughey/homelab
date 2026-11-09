# Weekly Maintenance
## Infrastructure

```
ansible-playbook ansible/playbooks/update-infrastructure.yml -K
```

## Kubernetes Workers

```
ansible-playbook ansible/playbooks/update-k8s-workers.yml -K
```

## Verify Cluster

```
kubectl get nodes kubectl get pods -A
```

## Control Plane

```
ansible-playbook ansible/playbooks/update-k8s-control.yml -K
```

#  Final Validation
```
kubectl get nodes kubectl get pods -A
```
