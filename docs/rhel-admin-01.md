# rhel-admin-01.lab.local
## Purpose

Administration host for:

- Ansible
- Git
- Podman
- kubectl
- Helm

## VM Specification

```
Hostname: rhel-admin-01.lab.local
IP: 10.2.0.210
vCPU: 2
RAM: 4GB
Disk: 40GB
OS: RHEL 10
```

## Build Process
### Install OS
RHEL 10 Minimal

### Hostname Configuration

```
sudo hostnamectl set-hostname rhel-admin-01.lab.local
```

### Update the OS

```
sudo dnf update -y
```

### Install Base System Packages

```
sudo dnf install -y \
git \
vim \
tmux \
curl \
wget \
jq \
bind-utils \
bash-completion \
ansible-core \
podman \
buildah \
qemu-guest-agent
```

### Enable Guest Agent

```
sudo systemctl enable --now qemu-guest-agent
```

### Verification

```
getenforce
firewall-cmd --state
ansible --version
podman --version
```

### Current Status
- Operational
- Joined to IPA
- Using IPA DNS

