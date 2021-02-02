# Assisted Installer Playbooks for OpenShift 4.x

**WARNING:** *This repo is currently a WIP!*

This repository has been created for the deployment of OCP 4.x using the Assisted Service. When completed, it should have everything needed to deploy Assisted Service (either using Podman or OpenShift), and manage the deployment of OCP clusters.

## TDLR:

Good examples of how these atomic playbooks can be run can be found in the following playbooks:
- `ansible-playbook -i inventory/jinkit.yml 00-createAll.yml -vv`
- `ansible-playbook -i inventory/jinkit.yml 00-deleteAll.yml -vv`

I will start fully documenting these playbooks this week, because right now it would appear that it's a mess.

BE AWARE: I have experienced a rare scenario where Libvirt will not honor the autostart flag (as intended). I will figure this out and document it accordingly. It is rare, but if you notice that hosts aren't advancing past "Installing 4/7" you may want to look to see if the Libvirt guests have been unintentionally shut down. Restarting them will often correct this issue.

DO NOT READ ANYTHING BEYOND THIS NOTE. I AM REWORKING THE DOCS SECTION.

#### IMPORTANT: Record the clusterID to Variable
```
clusterID=""
```

**Exaample:**
```
❯ curl -s  "http://ai.openshift.jinkit.com:8888/api/assisted-install/v1/clusters/" | jq ".[] | {id, name: .name}"
{
  "id": "aacdd8ae-9f51-4f4f-9ed7-ccd381c7f55d",
  "name": "customer-001-gx12my"
}

CURRENT_CLUSTER_ID="aacdd8ae-9f51-4f4f-9ed7-ccd381c7f55d"
```

### Managing Libvirt Guests

#### Creating/Starting
See [`libvirtGuest` Management](./docs/libvirtGuest.md#sub-section) documentation.

#### Deleting/Destroying
See [`libvirtGuest` Management](./docs/libvirtGuest.md#sub-section) documentation.



















#### Cleaning Up
You may want to remove directories and files left around after testing. These are stored in a directory called `.clusters` at the root of the project folder:
```
rm -rf .clusters/*
```

## Alternative Options




### Assisted Service Installation

#### AI Installation
```
ansible-playbook -i inventory/jinkit.yml createAssistedInstaller.yml -vv 
```

#### AI Removal
```
ansible-playbook -i inventory/jinkit.yml deleteAssistedInstaller.yml -vv --tags deleteAI
```


