#### Libvirt: Create libvirtHost on libvirtGuest
```
fileRemoteISO="/var/lib/libvirt/boot/ai-discovery-${clusterID}.iso"
libvirtHostName="kubenode01.jinkit.com"
libvirtGuestName="kubenode21"
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
libvirtGuestNetworkMAC="0e:00:00:03:60:21"
libvirtGuestNetworkBridge="br60"
libvirtGuestNetworkModel="virtio"
libvirtGuestGraphicsVNCPort="5921"
libvirtGuestGraphicsVNCListen="0.0.0.0"
libvirtGuestGraphicsVNCPassword="redhat"
libvirtGuestLogFile="/root/${libvirtGuestName}_install.log"


ansible-playbook -i inventory/jinkit.yml \
--limit ${libvirtHostName} 71-createAILibvirtGuest.yml \
--extra-vars "clusterID=${clusterID}" \
--extra-vars "fileLocalISO=${fileLocalISO}" \
--extra-vars "fileRemoteISO=${fileRemoteISO}" \
--extra-vars "libvirtGuestName=${libvirtGuestName}" \
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

#### Continue to 2
```
libvirtHostName="kubenode02.jinkit.com"
libvirtGuestName="kubenode22"
libvirtGuestNetworkMAC="0e:00:00:03:60:22"
libvirtGuestGraphicsVNCPort="5922"
libvirtGuestDiskPath="/var/lib/libvirt/images/${libvirtGuestName}.qcow2"
libvirtGuestLogFile="/root/${libvirtGuestName}_install.log"

ansible-playbook -i inventory/jinkit.yml \
--limit ${libvirtHostName} 71-createAILibvirtGuest.yml \
--extra-vars "clusterID=${clusterID}" \
--extra-vars "fileLocalISO=${fileLocalISO}" \
--extra-vars "fileRemoteISO=${fileRemoteISO}" \
--extra-vars "libvirtGuestName=${libvirtGuestName}" \
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

#### Continue to 3
```
libvirtHostName="kubenode03.jinkit.com"
libvirtGuestName="kubenode23"
libvirtGuestNetworkMAC="0e:00:00:03:60:23"
libvirtGuestGraphicsVNCPort="5923"
libvirtGuestDiskPath="/var/lib/libvirt/images/${libvirtGuestName}.qcow2"
libvirtGuestLogFile="/root/${libvirtGuestName}_install.log"

ansible-playbook -i inventory/jinkit.yml \
--limit ${libvirtHostName} 71-createAILibvirtGuest.yml \
--extra-vars "clusterID=${clusterID}" \
--extra-vars "fileLocalISO=${fileLocalISO}" \
--extra-vars "fileRemoteISO=${fileRemoteISO}" \
--extra-vars "libvirtGuestName=${libvirtGuestName}" \
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

#### Libvirt: Delete libvirtHost on libvirtGuest
```
libvirtHostName="kubenode01.jinkit.com"
libvirtGuestName="kubenode21"
ansible-playbook -i inventory/jinkit.yml --limit ${libvirtHostName} 61-deleteAILibvirtGuest.yml --extra-vars "libvirtGuest=${libvirtGuestName}" -i ${libvirtHostName} -vv
```

#### Continue to 2
```
libvirtHostName="kubenode02.jinkit.com"
libvirtGuestName="kubenode22"
ansible-playbook -i inventory/jinkit.yml --limit ${libvirtHostName} 61-deleteAILibvirtGuest.yml --extra-vars "libvirtGuest=${libvirtGuestName}" -i ${libvirtHostName} -vv
```

#### Continue to 3
```
libvirtHostName="kubenode03.jinkit.com"
libvirtGuestName="kubenode23"
ansible-playbook -i inventory/jinkit.yml --limit ${libvirtHostName} 61-deleteAILibvirtGuest.yml --extra-vars "libvirtGuest=${libvirtGuestName}" -i ${libvirtHostName} -vv
```