# Introduction

#### Artifacts
This will create artifacts which describe the cluster by the `clusterID`. For example:
```
cat .clusters/${clusterID}/${clusterID}.json | jq .
```

#### Generate Installation Media (ISO)
To then generate and download an ISO for this cluster, run the following playbook:
```
ansible-playbook -i inventory/jinkit.yml 02-downloadAIClusterISO.yml --extra-vars "clusterID=${clusterID}" -vv
```

*Two important files will also be created from this ISO generation, which we will copy from the Assisted Installer service API:*
```
cat ./.clusters/${clusterID}/files/discovery-ignition | jq .
cat ./.clusters/${clusterID}/files/install-config | jq .
```

#### Upload the ISO to Libvirt Hosts
```
ansible-playbook -i inventory/jinkit.yml 50-uploadAIClusterISO.yml --extra-vars "clusterID=${clusterID}" -vv
```