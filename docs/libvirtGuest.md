# Introduction
This document is intended to serve as a reference for the playbooks related to `libvirtGuests`.

### Creating a libvirtGuest
Creating a `libvirtGuest` can be achieved by atomic management-related tasks. The first task is intended to generate `libvirtGuest` templates written in [BASH](https://en.wikipedia.org/wiki/Bash_(Unix_shell)). The second is to then execute those scripts.

#### Creating a `libvirtGuest` Template

##### Lab Details
There are a few really important details about my personal lab, which may make this utility useful for the masses. It is very important to see my Lab Documentation section, so you understand why these settings work for me. I will make this more useful in the future, and increase the overall project scope, so long as this utility will work the same for my environment.

##### Prerequisites
- Cluster Creation (playbook: `createAICluster`)
- Generate ISO (playbook: `downloadAIClusterISO`)
- ISO exists on the target `libvirtHost` (playbook: `uploadAIClusterISO`)

It is important to create the following shell variable first, considering the target `clusterID`. If your intention is to create a host from an Assisted Service API this valuable is required. This utility doesn't have to apply only to OCP AI hosts, but this falls outside the scope of this documentation.

```
clusterID="fd352877-8a71-4dfd-8e21-e057a2f9ec13"
```

##### Examples
Please note the example below, which includes a 3 member OCP cluster. First, modify the following variables to match your scenario. The following example will consider three hosts:
- kubenode24
- kubenode25
- kubenode26

**Example:** kubenode24
```
dirRemoteLibvirtBase="/opt/ocp-demos/libvirt/guests"
dirRemoteLibvirtBoot="/var/lib/libvirt/boot"
dirRemoteLibvirtImages="/var/lib/libvirt/images"
fileLocalISO="./.clusters/${clusterID}/${clusterID}.iso"
fileRemoteISO="${dirRemoteLibvirtBoot}/ai-discovery-${clusterID}.iso"
fileRemoteLibvirtGuestLog="${dirRemoteLibvirtBase}/${libvirtGuestName}/${libvirtGuestName}.log"
libvirtHostName="kubenode04.jinkit.com"
libvirtGuestName="kubenode24"
libvirtGuestExecutionDelay="5"
libvirtGuestVirtType="kvm"
libvirtGuestComputeMemory="16384"
libvirtGuestComputeVCPUs="4"
libvirtGuestAccelerate="True"
libvirtGuestAutoStart="True"
libvirtGuestOSVariant="rhel8.3"
libvirtGuestDiskCDROM="/var/lib/libvirt/boot/ai-discovery-${clusterID}.iso"
libvirtGuestDiskPath="/var/lib/libvirt/images/${libvirtGuestName}.qcow2"
libvirtGuestDiskSize="120"
libvirtGuestDiskBus="virtio"
libvirtGuestDiskFormat="qcow2"
libvirtGuestNetworkMAC="0e:00:00:03:60:24"
libvirtGuestNetworkBridge="br60"
libvirtGuestNetworkModel="virtio"
libvirtGuestGraphicsVNCPort="5924"
libvirtGuestGraphicsVNCListen="0.0.0.0"
libvirtGuestGraphicsVNCPassword="redhat"

# RUN IT:
ansible-playbook -i inventory/jinkit.yml \
--limit ${libvirtHostName} 52-createAILibvirtGuestTemplates.yml \
--extra-vars "dirRemoteLibvirtBase=${dirRemoteLibvirtBase}" \
--extra-vars "dirRemoteLibvirtBoot=${dirRemoteLibvirtBoot}" \
--extra-vars "dirRemoteLibvirtImages=${dirRemoteLibvirtImages}" \
--extra-vars "fileLocalISO=${fileLocalISO}" \
--extra-vars "fileRemoteISO=${fileRemoteISO}" \
--extra-vars "fileRemoteLibvirtGuestLog=${fileRemoteLibvirtGuestLog}" \
--extra-vars "libvirtHostName=${libvirtHostName}" \
--extra-vars "libvirtGuestName=${libvirtGuestName}" \
--extra-vars "libvirtGuestExecutionDelay=${libvirtGuestExecutionDelay}" \
--extra-vars "libvirtGuestVirtType=${libvirtGuestVirtType}" \
--extra-vars "libvirtGuestComputeMemory=${libvirtGuestComputeMemory}" \
--extra-vars "libvirtGuestComputeVCPUs=${libvirtGuestComputeVCPUs}" \
--extra-vars "libvirtGuestAccelerate=${libvirtGuestAccelerate}" \
--extra-vars "libvirtGuestAutoStart=${libvirtGuestAutoStart}" \
--extra-vars "libvirtGuestOSVariant=${libvirtGuestOSVariant}" \
--extra-vars "libvirtGuestDiskCDROM=${libvirtGuestDiskCDROM}" \
--extra-vars "libvirtGuestDiskPath=${libvirtGuestDiskPath}" \
--extra-vars "libvirtGuestDiskSize=${libvirtGuestDiskSize}" \
--extra-vars "libvirtGuestDiskBus=${libvirtGuestDiskBus}" \
--extra-vars "libvirtGuestDiskFormat=${libvirtGuestDiskFormat}" \
--extra-vars "libvirtGuestNetworkMAC=${libvirtGuestNetworkMAC}" \
--extra-vars "libvirtGuestNetworkBridge=${libvirtGuestNetworkBridge}" \
--extra-vars "libvirtGuestNetworkModel=${libvirtGuestNetworkModel}" \
--extra-vars "libvirtGuestGraphicsVNCPort=${libvirtGuestGraphicsVNCPort}" \
--extra-vars "libvirtGuestGraphicsVNCListen=${libvirtGuestGraphicsVNCListen}" \
--extra-vars "libvirtGuestGraphicsVNCPassword=${libvirtGuestGraphicsVNCPassword}" \
-i ${libvirtHostName} -vv
```

**Example:** kubenode25
```
libvirtHostName="kubenode05.jinkit.com"
libvirtGuestName="kubenode25"
libvirtGuestNetworkMAC="0e:00:00:03:60:25"
libvirtGuestGraphicsVNCPort="5925"

# RUN IT:
ansible-playbook -i inventory/jinkit.yml \
--limit ${libvirtHostName} 52-createAILibvirtGuestTemplates.yml \
--extra-vars "dirRemoteLibvirtBase=${dirRemoteLibvirtBase}" \
--extra-vars "dirRemoteLibvirtBoot=${dirRemoteLibvirtBoot}" \
--extra-vars "dirRemoteLibvirtImages=${dirRemoteLibvirtImages}" \
--extra-vars "fileLocalISO=${fileLocalISO}" \
--extra-vars "fileRemoteISO=${fileRemoteISO}" \
--extra-vars "fileRemoteLibvirtGuestLog=${fileRemoteLibvirtGuestLog}" \
--extra-vars "libvirtHostName=${libvirtHostName}" \
--extra-vars "libvirtGuestName=${libvirtGuestName}" \
--extra-vars "libvirtGuestExecutionDelay=${libvirtGuestExecutionDelay}" \
--extra-vars "libvirtGuestVirtType=${libvirtGuestVirtType}" \
--extra-vars "libvirtGuestComputeMemory=${libvirtGuestComputeMemory}" \
--extra-vars "libvirtGuestComputeVCPUs=${libvirtGuestComputeVCPUs}" \
--extra-vars "libvirtGuestAccelerate=${libvirtGuestAccelerate}" \
--extra-vars "libvirtGuestAutoStart=${libvirtGuestAutoStart}" \
--extra-vars "libvirtGuestOSVariant=${libvirtGuestOSVariant}" \
--extra-vars "libvirtGuestDiskCDROM=${libvirtGuestDiskCDROM}" \
--extra-vars "libvirtGuestDiskPath=${libvirtGuestDiskPath}" \
--extra-vars "libvirtGuestDiskSize=${libvirtGuestDiskSize}" \
--extra-vars "libvirtGuestDiskBus=${libvirtGuestDiskBus}" \
--extra-vars "libvirtGuestDiskFormat=${libvirtGuestDiskFormat}" \
--extra-vars "libvirtGuestNetworkMAC=${libvirtGuestNetworkMAC}" \
--extra-vars "libvirtGuestNetworkBridge=${libvirtGuestNetworkBridge}" \
--extra-vars "libvirtGuestNetworkModel=${libvirtGuestNetworkModel}" \
--extra-vars "libvirtGuestGraphicsVNCPort=${libvirtGuestGraphicsVNCPort}" \
--extra-vars "libvirtGuestGraphicsVNCListen=${libvirtGuestGraphicsVNCListen}" \
--extra-vars "libvirtGuestGraphicsVNCPassword=${libvirtGuestGraphicsVNCPassword}" \
-i ${libvirtHostName} -vv
```

**Example:** kubenode26
```
libvirtHostName="kubenode06.jinkit.com"
libvirtGuestName="kubenode26"
libvirtGuestNetworkMAC="0e:00:00:03:60:26"
libvirtGuestGraphicsVNCPort="5926"

# RUN IT:
ansible-playbook -i inventory/jinkit.yml \
--limit ${libvirtHostName} 52-createAILibvirtGuestTemplates.yml \
--extra-vars "dirRemoteLibvirtBase=${dirRemoteLibvirtBase}" \
--extra-vars "dirRemoteLibvirtBoot=${dirRemoteLibvirtBoot}" \
--extra-vars "dirRemoteLibvirtImages=${dirRemoteLibvirtImages}" \
--extra-vars "fileLocalISO=${fileLocalISO}" \
--extra-vars "fileRemoteISO=${fileRemoteISO}" \
--extra-vars "fileRemoteLibvirtGuestLog=${fileRemoteLibvirtGuestLog}" \
--extra-vars "libvirtHostName=${libvirtHostName}" \
--extra-vars "libvirtGuestName=${libvirtGuestName}" \
--extra-vars "libvirtGuestExecutionDelay=${libvirtGuestExecutionDelay}" \
--extra-vars "libvirtGuestVirtType=${libvirtGuestVirtType}" \
--extra-vars "libvirtGuestComputeMemory=${libvirtGuestComputeMemory}" \
--extra-vars "libvirtGuestComputeVCPUs=${libvirtGuestComputeVCPUs}" \
--extra-vars "libvirtGuestAccelerate=${libvirtGuestAccelerate}" \
--extra-vars "libvirtGuestAutoStart=${libvirtGuestAutoStart}" \
--extra-vars "libvirtGuestOSVariant=${libvirtGuestOSVariant}" \
--extra-vars "libvirtGuestDiskCDROM=${libvirtGuestDiskCDROM}" \
--extra-vars "libvirtGuestDiskPath=${libvirtGuestDiskPath}" \
--extra-vars "libvirtGuestDiskSize=${libvirtGuestDiskSize}" \
--extra-vars "libvirtGuestDiskBus=${libvirtGuestDiskBus}" \
--extra-vars "libvirtGuestDiskFormat=${libvirtGuestDiskFormat}" \
--extra-vars "libvirtGuestNetworkMAC=${libvirtGuestNetworkMAC}" \
--extra-vars "libvirtGuestNetworkBridge=${libvirtGuestNetworkBridge}" \
--extra-vars "libvirtGuestNetworkModel=${libvirtGuestNetworkModel}" \
--extra-vars "libvirtGuestGraphicsVNCPort=${libvirtGuestGraphicsVNCPort}" \
--extra-vars "libvirtGuestGraphicsVNCListen=${libvirtGuestGraphicsVNCListen}" \
--extra-vars "libvirtGuestGraphicsVNCPassword=${libvirtGuestGraphicsVNCPassword}" \
-i ${libvirtHostName} -vv
```

#### Start Libvirt Guest
Since a bulk of the `libvirtGuest` details were created as part of a startup template, our actual script execution is very straightforward. The only definitions that are needed are to tell Ansible which `libvirtGuestName` exists on `libvirtHostName`. As long as none of your other directory or file definitions have changed, you can run the following (example).

**Example:** kubenode24
```
libvirtHostName="kubenode04.jinkit.com"
libvirtGuestName="kubenode24"

ansible-playbook -i inventory/jinkit.yml \
--limit ${libvirtHostName} 53-startAILibvirtGuest.yml \
--extra-vars "dirRemoteLibvirtBase=${dirRemoteLibvirtBase}" \
--extra-vars "libvirtGuestName=${libvirtGuestName}" \
-i ${libvirtHostName} -vv
```

**Example:** kubenode25
```
libvirtHostName="kubenode05.jinkit.com"
libvirtGuestName="kubenode25"

ansible-playbook -i inventory/jinkit.yml \
--limit ${libvirtHostName} 53-startAILibvirtGuest.yml \
--extra-vars "dirRemoteLibvirtBase=${dirRemoteLibvirtBase}" \
--extra-vars "libvirtGuestName=${libvirtGuestName}" \
-i ${libvirtHostName} -vv
```

**Example:** kubenode26
```
libvirtHostName="kubenode06.jinkit.com"
libvirtGuestName="kubenode26"

ansible-playbook -i inventory/jinkit.yml \
--limit ${libvirtHostName} 53-startAILibvirtGuest.yml \
--extra-vars "dirRemoteLibvirtBase=${dirRemoteLibvirtBase}" \
--extra-vars "libvirtGuestName=${libvirtGuestName}" \
-i ${libvirtHostName} -vv
```
[Return to README](../README.md#sub-section)


#### Delete Libvirt Guest
Deletion of the `libvirtGuest` is the same as initial execution/creation.

**Example:** kubenode24
```
libvirtHostName="kubenode04.jinkit.com"
libvirtGuestName="kubenode24"

ansible-playbook -i inventory/jinkit.yml \
--limit ${libvirtHostName} 61-deleteAILibvirtGuest.yml \
--extra-vars "dirRemoteLibvirtBase=${dirRemoteLibvirtBase}" \
--extra-vars "libvirtGuestName=${libvirtGuestName}" \
-i ${libvirtHostName} -vv
```

**Example:** kubenode25
```
libvirtHostName="kubenode05.jinkit.com"
libvirtGuestName="kubenode25"

ansible-playbook -i inventory/jinkit.yml \
--limit ${libvirtHostName} 61-deleteAILibvirtGuest.yml \
--extra-vars "dirRemoteLibvirtBase=${dirRemoteLibvirtBase}" \
--extra-vars "libvirtGuestName=${libvirtGuestName}" \
-i ${libvirtHostName} -vv
```

**Example:** kubenode26
```
libvirtHostName="kubenode06.jinkit.com"
libvirtGuestName="kubenode26"

ansible-playbook -i inventory/jinkit.yml \
--limit ${libvirtHostName} 61-deleteAILibvirtGuest.yml \
--extra-vars "dirRemoteLibvirtBase=${dirRemoteLibvirtBase}" \
--extra-vars "libvirtGuestName=${libvirtGuestName}" \
-i ${libvirtHostName} -vv
```

#### Remove Libvirt Guest Template
If you need to remove the `libvirtGuest` template entirely, you can execute the following Ansible playbook. Remember to define the directory where you've placed the execution (create/delete) scripts.

**Example:** kubenode24
```
libvirtHostName="kubenode04.jinkit.com"
libvirtGuestName="kubenode24"
dirRemoteLibvirtBase="/opt/ocp-demos/libvirt/guests"

ansible-playbook -i inventory/jinkit.yml \
--limit ${libvirtHostName} 62-deleteAILibvirtGuestTemplates.yml \
--extra-vars "dirRemoteLibvirtBase=${dirRemoteLibvirtBase}" \
--extra-vars "libvirtGuestName=${libvirtGuestName}" \
-i ${libvirtHostName} -vv
```

**Example:** kubenode25
```
libvirtHostName="kubenode05.jinkit.com"
libvirtGuestName="kubenode25"
dirRemoteLibvirtBase="/opt/ocp-demos/libvirt/guests"

ansible-playbook -i inventory/jinkit.yml \
--limit ${libvirtHostName} 62-deleteAILibvirtGuestTemplates.yml \
--extra-vars "dirRemoteLibvirtBase=${dirRemoteLibvirtBase}" \
--extra-vars "libvirtGuestName=${libvirtGuestName}" \
-i ${libvirtHostName} -vv
```

**Example:** kubenode26
```
libvirtHostName="kubenode06.jinkit.com"
libvirtGuestName="kubenode26"
dirRemoteLibvirtBase="/opt/ocp-demos/libvirt/guests"

ansible-playbook -i inventory/jinkit.yml \
--limit ${libvirtHostName} 62-deleteAILibvirtGuestTemplates.yml \
--extra-vars "dirRemoteLibvirtBase=${dirRemoteLibvirtBase}" \
--extra-vars "libvirtGuestName=${libvirtGuestName}" \
-i ${libvirtHostName} -vv
```

[Return to README](../README.md)