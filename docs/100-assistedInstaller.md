# Introduction

### Create a New Cluster (with variables)
```
clusterName="testing"
clusterVersion="4.6"
clusterBaseDomain="jinkit.com"
clusterEndpointIPAPI="192.168.60.30"
clusterEndpointIPAPIDHCP="false"
clusterEndpointIPIngress="192.168.60.31"
clusterEndpointIPIngressDHCP="false"
clusterNetworkUserManaged="false"
clusterNetworkCIDRPod="10.128.0.0/14"
clusterNetworkCIDRService="172.30.0.0/16"

ansible-playbook -i inventory/sample-inventory.yml \
--extra-vars "clusterName=${clusterName}" \
--extra-vars "clusterVersion=${clusterVersion}" \
--extra-vars "clusterBaseDomain=${clusterBaseDomain}" \
--extra-vars "clusterEndpointIPAPI=${clusterEndpointIPAPI}" \
--extra-vars "clusterEndpointIPAPIDHCP=${clusterEndpointIPAPIDHCP}" \
--extra-vars "clusterEndpointIPIngress=${clusterEndpointIPIngress}" \
--extra-vars "clusterEndpointIPIngressDHCP=${clusterEndpointIPIngressDHCP}" \
--extra-vars "clusterNetworkUserManaged=${clusterNetworkUserManaged}" \
--extra-vars "clusterNetworkCIDRPod=${clusterNetworkCIDRPod}" \
--extra-vars "clusterNetworkCIDRService=${clusterNetworkCIDRService}" \
01-createAICluster.yml -vv
```

***NOTE:*** *I need to work on the following variable, with the way that Ansible handles this int*<br>
`--extra-vars 'clusterNetworkHostPrefix=\"24\"' \`

#### List Clusters (via cURL)
List existing clusters and their corresponding names with the following:
```
curl -s  "http://ai.openshift.jinkit.com:8888/api/assisted-install/v1/clusters/" | jq ".[] | {id, name: .name}"
```

#### Deleting a Cluster (with variables)
To delete a cluster:
```
ansible-playbook -i inventory/jinkit.yml 90-deleteAICluster.yml --extra-vars "clusterID=${clusterID}" -vv
```