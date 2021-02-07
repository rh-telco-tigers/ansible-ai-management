# Introduction
This playbook is created for Ansible 2.10+ clients. In order to use this playbook, you will need to install the `containers.podman` module.
```
ansible-galaxy collection install containers.podman
```

### Create a New Cluster (with variables)
Defaults _should_ be maintained, which would allow most users to leverage their own inventory file. Please see the sample inventory included with this project. This means that when using the sample inventory file, this playbook would be run like:
```
ansible-playbook -i inventory/sample-inventory.yml \
000-createAssistedInstaller.yml -vv --limit "assistedInstaller"
```

However, there can be cases where some defaults are out of date. One common mistake that can be made is to overlook the `sha256sum` hash for the RHCOS LiveISO. To override this value, see the notes below and run like so:
```
RHCOS_LIVEISO_CHK="b264d398cce0affca218ee56808332d90b7c0a6dac2c061effdfa834a86623ba"

ansible-playbook -i inventory/sample-inventory.yml \
--extra-vars "RHCOS_LIVEISO_CHK=${RHCOS_LIVEISO_CHK}" \
000-createAssistedInstaller.yml -vv --limit "assistedInstaller"
```

***NOTE:*** *Address any additional notes here*<br>
`--extra-vars "RHCOS_LIVEISO_CHK=${RHCOS_LIVEISO_CHK}"` will correct any `sha256sum` mismatch issues. See below for more details.

#### Deleting an AI Installation (using variables)
To delete the Assisted Installer installation, perform the following:
```
ansible-playbook -i inventory/sample-inventory.yml
```

If you wish to force remove the directory created for Assisted Installer (`/opt/assisted-installer`) then use the variable `forceClean=true`.
```
ansible-playbook -i inventory/sample-inventory.yml \                                                                                                                                                     ─╯
--extra-vars "forceClean=true" \                       
000-deleteAssistedInstaller.yml -vv --limit "assistedInstaller"
```

#### Troubleshooting

**Downloading the RHCOS LiveISO**
```
TASK [configureAssistedInstaller : Download the RHCOS LiveCD] *************************************************************************************************************************************************
task path: /Users/bjozsa/Documents/Red Hat/Demos/Technology/Assisted-Installer/ansible/github.com/v1k0d3n/ansible-ai-management/roles/configureAssistedInstaller/tasks/main.yml:98
fatal: [ai.openshift.jinkit.com]: FAILED! => changed=true 
  checksum_dest: 0f03ad54d39357b8aa087325dda1e424a557bbf5
  checksum_src: f4adc9fe17876cc8a81fe4d2c09a1c2b1870eca2
  dest: /opt/assisted-service/rhcos-live.x86_64.iso
  elapsed: 14
  msg: The checksum for /opt/assisted-service/rhcos-live.x86_64.iso did not match 4bb81d88c66923f6ad46856783ee8e57bf1bbabf0f1ae3ae0b2c2e60101c6832; it was b264d398cce0affca218ee56808332d90b7c0a6dac2c061effdfa834a86623ba.
  src: /home/cloud-user/.ansible/tmp/ansible-tmp-1612717964.3857548-93956-39047464216848/tmp612b5rl2
  url: https://mirror.openshift.com/pub/openshift-v4/x86_64/dependencies/rhcos/pre-release/latest-4.7/rhcos-live.x86_64.iso
```

This most likely occurs when the `sha256` hash does not match what's been provide. This comes up more often for in-development releases, or pre-releases (as of writing, pre-release 4.7). You can avoid this by using the correct has provided at `https://mirror.openshift.com/pub/openshift-v4/x86_64/dependencies/rhcos/<RELEASE>/<VERSION>/sha256sum.txt` and using the appropriate `sha256`. To override this value using variables, perform the following:
```
RHCOS_LIVEISO_CHK="b264d398cce0affca218ee56808332d90b7c0a6dac2c061effdfa834a86623ba"

ansible-playbook -i inventory/sample-inventory.yml \
--extra-vars "RHCOS_LIVEISO_CHK=${RHCOS_LIVEISO_CHK}" \
000-createAssistedInstaller.yml -vv --limit "assistedInstaller"
```

#### TODO
- clean up the default values