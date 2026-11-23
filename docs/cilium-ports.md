## Additional Cilium Firewall Requirements

When using Cilium in VXLAN mode:

- UDP 8472 must be permitted between nodes.
- TCP 4240 must be permitted between nodes.
- UDP 4240 must be permitted between nodes.

Failure to open these ports can result in:

- Cilium cluster health failures
- Cross-node pod communication issues
- Kubernetes webhook failures
- MetalLB installation/configuration problems
