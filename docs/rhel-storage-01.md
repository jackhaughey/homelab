# rhel-storage-01.lab.local
## Purpose

Provides NFS-backed storage for Kubernetes.

## VM Specification

```
Hostname: rhel-storage-01.lab.local
IP: 10.2.0.211

2 vCPU
8GB RAM

Disk 1: 40GB OS
Disk 2: 200GB Storage
```

## Build Process
### Create Physical Volume

```
sudo pvcreate /dev/sdb
```

### Create Volume Group

```
sudo vgcreate vg_storage /dev/sdb
```

### Create Logical Volumes

```
sudo lvcreate -L 50G -n lv_apps vg_storage
sudo lvcreate -L 50G -n lv_media vg_storage
sudo lvcreate -L 50G -n lv_backups vg_storage
```

### Create Filesystems

```
sudo mkfs.xfs /dev/vg_storage/lv_apps
sudo mkfs.xfs /dev/vg_storage/lv_media
sudo mkfs.xfs /dev/vg_storage/lv_backups
```

### Create Mount Points

```
/srv/apps
/srv/media
/srv/backups
```

### Configure Network File Services

```
sudo systemctl enable --now nfs-server
```

### Configure Exports

```
/srv/apps
/srv/media
/srv/backups
```

### Configure The Firewall

```
sudo firewall-cmd --permanent --add-service=nfs
sudo firewall-cmd --permanent --add-service=rpc-bind
sudo firewall-cmd --permanent --add-service=mountd
```

### Configure SELiux

Allows SELinux to permit read/write access to files and directories exported through NFS while keeping SELinux in Enforcing mode.

```
sudo setsebool -P nfs_export_all_rw 1
```

### Current Status

```
Operational
NFS exports available
Joined to IPA
```


