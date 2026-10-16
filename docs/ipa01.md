# ipa01.lab.local
## Purpose

Identity management, DNS and Kerberos.

VM Specification

```
Hostname: ipa01.lab.local
IP: 10.2.0.212

2 vCPU
8GB RAM
60GB Disk

OS:
Rocky Linux 10
```

## Build Process
### Install Packages

```
sudo dnf install -y \
freeipa-server \
freeipa-server-dns
```

### Install IPA

```
sudo ipa-server-install \
--hostname=ipa01.lab.local \
--setup-dns
```

Configuration;

```
Domain:
lab.local

Realm:
LAB.LOCAL

DNS:
Integrated BIND

Forwarders:
10.1.0.2
10.2.0.1
```

### Firewall Configuration

```
sudo firewall-cmd --permanent --add-service=http
sudo firewall-cmd --permanent --add-service=https
sudo firewall-cmd --permanent --add-service=dns
sudo firewall-cmd --permanent --add-service=ldap
sudo firewall-cmd --permanent --add-service=ldaps
sudo firewall-cmd --permanent --add-service=kerberos
```

### Create DNS Records 

```
rhel-admin-01
10.2.0.210

rhel-storage-01
10.2.0.211
```

### Join Clients

On these servers;

```
rhel-admin-01
rhel-storage-0
```

Perform;

```
sudo ipa-client-install
```

## Current State

```
Operational
DNS Active
LDAP Active
Kerberos Active
Clients Joined
```


