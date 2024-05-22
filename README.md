# promox

## Pass thru hdd/sdd
https://pve.proxmox.com/wiki/Passthrough_Physical_Disk_to_Virtual_Machine_(VM)

### Listing by id
```
lsblk |awk 'NR==1{print $0" DEVICE-ID(S)"}NR>1{dev=$1;printf $0" ";system("find /dev/disk/by-id -lname \"*"dev"\" -printf \" %p\"");print "";}'|grep -v -E 'part|lvm'
```
### Hot-Plug/Add physical device as new virtual SCSI disk

```
qm set 592 -scsi2 /dev/disk/by-id/ata-ST3000DM001-1CH166_Z1F41BLC
update VM 592: -scsi2 /dev/disk/by-id/ata-ST3000DM001-1CH166_Z1F41BLC

```

### Hot-Unplug/Remove virtual disk

```
qm unlink 592 --idlist scsi2
update VM 592: -delete scsi2
```

