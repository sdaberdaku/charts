# karpenter-extra

![Version: 1.0.0](https://img.shields.io/badge/Version-1.0.0-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 1.0.3](https://img.shields.io/badge/AppVersion-1.0.3-informational?style=flat-square)

A chart for managing Karpenter NodeClasses and NodePools

## Maintainers

| Name | Email | Url |
| ---- | ------ | --- |
| Sebastian Daberdaku | <sebastiandaberdaku@gmail.com> |  |

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| nameOverride | string | `""` |  |
| fullnameOverride | string | `""` |  |
| eksClusterName | string | `"my-eks-cluster"` |  |
| nodeClasses.default.amiFamily | string | `"AL2"` |  |
| nodeClasses.default.detailedMonitoring | bool | `false` |  |
| nodeClasses.default.blockDeviceMappings[0].deviceName | string | `"/dev/xvda"` |  |
| nodeClasses.default.blockDeviceMappings[0].ebs.volumeSize | string | `"50Gi"` |  |
| nodeClasses.default.blockDeviceMappings[0].ebs.volumeType | string | `"gp3"` |  |
| nodeClasses.default.blockDeviceMappings[0].ebs.encrypted | bool | `true` |  |
| nodeClasses.default.blockDeviceMappings[0].ebs.deleteOnTermination | bool | `true` |  |
| nodeClasses.default.tags.test | string | `"value"` |  |
| nodeClasses.default.tags.test2 | string | `"value2"` |  |
| nodeClasses.default.userData | string | `"#! /bin/bash\necho \"Hello, World!\"\n"` |  |
| nodeClasses.large-ephemeral-storage.detailedMonitoring | bool | `true` |  |
| nodeClasses.large-ephemeral-storage.blockDeviceMappings[0].deviceName | string | `"/dev/xvda"` |  |
| nodeClasses.large-ephemeral-storage.blockDeviceMappings[0].ebs.volumeSize | string | `"500Gi"` |  |
| nodeClasses.large-ephemeral-storage.blockDeviceMappings[0].ebs.volumeType | string | `"gp3"` |  |
| nodeClasses.large-ephemeral-storage.blockDeviceMappings[0].ebs.encrypted | bool | `true` |  |
| nodeClasses.large-ephemeral-storage.blockDeviceMappings[0].ebs.deleteOnTermination | bool | `true` |  |
| nodeClasses.multi-pv-nvme-instance-store.detailedMonitoring | bool | `true` |  |
| nodeClasses.multi-pv-nvme-instance-store.blockDeviceMappings[0].deviceName | string | `"/dev/xvda"` |  |
| nodeClasses.multi-pv-nvme-instance-store.blockDeviceMappings[0].ebs.volumeSize | string | `"50Gi"` |  |
| nodeClasses.multi-pv-nvme-instance-store.blockDeviceMappings[0].ebs.volumeType | string | `"gp3"` |  |
| nodeClasses.multi-pv-nvme-instance-store.blockDeviceMappings[0].ebs.encrypted | bool | `true` |  |
| nodeClasses.multi-pv-nvme-instance-store.blockDeviceMappings[0].ebs.deleteOnTermination | bool | `true` |  |
| nodeClasses.multi-pv-nvme-instance-store.userData | string | `"#! /bin/bash\n# Install NVMe CLI\nyum install nvme-cli -y\n# Get a list of instance-store NVMe drives\nnvme_drives=$(nvme list | grep \"Amazon EC2 NVMe Instance Storage\" | cut -d \" \" -f 1 || true)\nreadarray -t nvme_drives <<< \"$nvme_drives\"\nfor disk in \"${nvme_drives[@]}\"\ndo\n  # Format the disk to ext4\n  mkfs.ext4 -F $disk\n  # Get disk UUID\n  uuid=$(blkid -o value -s UUID $disk)\n  # Create a filesystem path to mount the disk\n  mount_location=\"/mnt/fast-disks/${uuid}\"\n  mkdir -p $mount_location\n  # Mount the disk\n  mount $disk $mount_location\n  # Mount the disk during a reboot\n  echo $disk $mount_location ext4 defaults,noatime 0 2 >> /etc/fstab\n  # Set permissions for read-write-execute on $mount_location\n  chmod -R 0777 $mount_location\ndone\n"` |  |
| nodeClasses.single-raid-pv-nvme-instance-store.detailedMonitoring | bool | `true` |  |
| nodeClasses.single-raid-pv-nvme-instance-store.blockDeviceMappings[0].deviceName | string | `"/dev/xvda"` |  |
| nodeClasses.single-raid-pv-nvme-instance-store.blockDeviceMappings[0].ebs.volumeSize | string | `"50Gi"` |  |
| nodeClasses.single-raid-pv-nvme-instance-store.blockDeviceMappings[0].ebs.volumeType | string | `"gp3"` |  |
| nodeClasses.single-raid-pv-nvme-instance-store.blockDeviceMappings[0].ebs.encrypted | bool | `true` |  |
| nodeClasses.single-raid-pv-nvme-instance-store.blockDeviceMappings[0].ebs.deleteOnTermination | bool | `true` |  |
| nodeClasses.single-raid-pv-nvme-instance-store.userData | string | `"#! /bin/bash\n# Install NVMe CLI\nyum install nvme-cli -y\n# Get list of NVMe Drives\nnvme_drives=$(nvme list | grep \"Amazon EC2 NVMe Instance Storage\" | cut -d \" \" -f 1 || true)\nreadarray -t nvme_drives <<< \"$nvme_drives\"\nnum_drives=${#nvme_drives[@]}\n# Install software RAID utility\nyum install mdadm -y\n# Create RAID-0 array across the instance store NVMe SSDs\nmdadm --create /dev/md0 --level=0 --name=md0 --raid-devices=$num_drives \"${nvme_drives[@]}\"\n# Format drive with Ext4\nmkfs.ext4 /dev/md0\n# Get RAID array's UUID\n# uuid=$(blkid -o value -s UUID /dev/md0)\n# Create a filesystem path to mount the disk\n# mount_location=\"/mnt/fast-disks/${uuid}\"\nmount_location=\"/mnt/fast-disks\"\nmkdir -p $mount_location\n# Mount RAID device\nmount /dev/md0 $mount_location\n# Have disk be mounted on reboot\nmdadm --detail --scan >> /etc/mdadm.conf\necho /dev/md0 $mount_location ext4 defaults,noatime 0 2 >> /etc/fstab\n# Set permissions for read-write-execute on $mount_location\nchmod -R 0777 $mount_location\n"` |  |
| nodePools.default.nodeClassName | string | `"default"` |  |
| nodePools.default.labels.dedicated | string | `"my-workload"` |  |
| nodePools.default.annotations.annotate | string | `"this"` |  |
| nodePools.default.taints[0].key | string | `"dedicated"` |  |
| nodePools.default.taints[0].operator | string | `"Equal"` |  |
| nodePools.default.taints[0].value | string | `"my-workload"` |  |
| nodePools.default.taints[0].effect | string | `"NoSchedule"` |  |
| nodePools.default.startupTaints[0].key | string | `"example.com/another-taint"` |  |
| nodePools.default.startupTaints[0].effect | string | `"NoSchedule"` |  |
| nodePools.default.requirements[0].key | string | `"karpenter.k8s.aws/instance-family"` |  |
| nodePools.default.requirements[0].operator | string | `"In"` |  |
| nodePools.default.requirements[0].values[0] | string | `"c5"` |  |
| nodePools.default.requirements[0].values[1] | string | `"r5"` |  |
| nodePools.default.requirements[0].values[2] | string | `"m5"` |  |
| nodePools.default.requirements[1].key | string | `"karpenter.sh/capacity-type"` |  |
| nodePools.default.requirements[1].operator | string | `"In"` |  |
| nodePools.default.requirements[1].values[0] | string | `"spot"` |  |
| nodePools.default.resourceLimits.cpu | string | `"10"` |  |
| nodePools.default.resourceLimits.ram | string | `"100Gi"` |  |
| nodePools.default.consolidationPolicy | string | `"WhenUnderutilized"` |  |
| nodePools.default.consolidateAfter | string | `"30s"` |  |
| nodePools.default.expireAfter | string | `"720h"` |  |
| nodePools.default.weight | int | `10` |  |
| nodePools.equalizer.nodeClassName | string | `"large-ephemeral-storage"` |  |
| nodePools.equalizer.labels.dedicated | string | `"equalizer"` |  |
| nodePools.equalizer.requirements[0].key | string | `"karpenter.k8s.aws/instance-family"` |  |
| nodePools.equalizer.requirements[0].operator | string | `"In"` |  |
| nodePools.equalizer.requirements[0].values[0] | string | `"c5"` |  |
| nodePools.equalizer.requirements[0].values[1] | string | `"r5"` |  |
| nodePools.equalizer.requirements[0].values[2] | string | `"m5"` |  |
| nodePools.equalizer.requirements[1].key | string | `"karpenter.sh/capacity-type"` |  |
| nodePools.equalizer.requirements[1].operator | string | `"In"` |  |
| nodePools.equalizer.requirements[1].values[0] | string | `"spot"` |  |
| nodePools.equalizer.resourceLimits.cpu | string | `"10"` |  |
| nodePools.equalizer.resourceLimits.ram | string | `"100Gi"` |  |
| nodePools.equalizer.consolidationPolicy | string | `"WhenUnderutilized"` |  |
| nodePools.equalizer.consolidateAfter | string | `"30s"` |  |
| nodePools.equalizer.expireAfter | string | `"720h"` |  |
| nodePools.equalizer.weight | int | `10` |  |

----------------------------------------------
Autogenerated from chart metadata using [helm-docs v1.14.2](https://github.com/norwoodj/helm-docs/releases/v1.14.2)
