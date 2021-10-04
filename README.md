# Install Red Hat Advanced Cluster Security for K8s in Openshift

Deploy Red Hat Advanced Cluster Security for Kubernetes Demo ( Apps and Pipelines ) on OpenShift 4.x in a easy and automated way.

## PREREQUISITES

### Ansible 2.9
- [Ansible Installation Guide](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html)
- PyYAML
- python3-openshift
- python3-jmespath


### Define variables for your cluster

| Variable | Description |
| -------- | -------- |
| ocp_username    | OpenShift Cluster Admin User  |
| ocp4_workload_stackrox_central_admin_password    | RHACS - Central Admin Password     |
| ocp4_workload_stackrox_central_orchestrator    |  crc or openshift ( full cluster )     |
| ACTION    | create ( To install ) or destroy ( To uninstall )  |


### Steps

#### Installing RHACS and Demo workloads
---
```
ansible-galaxy collection install kubernetes.core
git clone https://github.com/rcarrata/rhacs-demo
cd rhacs-demo
```

You can use the **rhacs-install.yaml** as example, please change the credentials before running the playbook.

rhacs-install.yaml file Example
---
```
- hosts: localhost
  vars:
    ocp_username: kubeadmin
    ocp4_workload_stackrox_central_admin_password: QHb7jH9SusmBmmQX
    ocp4_workload_stackrox_central_orchestrator: crc
    #ocp4_workload_stackrox_central_orchestrator: openshift
  roles:
  - ocp4_workload_stackrox_central
  - ocp4_workload_stackrox_sensor
  - ocp4_workload_stackrox_demo_apps
  - ocp4_workload_stackrox_demo_pipeline
```

Login to ocp using a Cluster-Admin user.
---
```
oc login -u admin https://yourcluster:6443
```

Running the playbook.
---
```
ansible-playbook rhacs-install.yaml
```

It might take a bit of time, so grab a coffee and enjoy :)


