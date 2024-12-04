# Agent CRs Generator
An ansible playbook for generating [Agent](https://github.com/openshift/assisted-service/blob/8984adf7a95fb149c3368dec9c3746c65f1e3664/vendor/github.com/openshift/assisted-service/api/v1beta1/agent_types.go#L287) CRs by querying installed OCP nodes.
The generator is needed for specific scenarios in which Agents are missing on OCP clusters after being imported to ACM.

## Requirements
* Ansible >= 2.15
* ACM >= 2.12

## Usage

### Configuration
Add the relevant BMHs list to [inventory.yml](./inventory.yml) file.
Each item should include the following:
```
ansible_host: < FQDN or IP of the host > -- Ensure SSH availability 
namespace: < Namespace of the Cluster >
role: < Role of the node: master/worker >
bmh_name: < Name of the BMH>
infraenv_name: < Name of the associated InfraEnv >
clusterdeployment_name: < Name of the associated ClusterdDeployment >
```

### Run
```
$ ansible-playbook -i inventory.yml main.yml
```

### Apply CRs
The Agent yaml files should be available under the `generated` folder.

Notes: 
* Apply the files on the ACM hub after upgrading to 2.12.
* Ensure the relevant resources are available for the associated cluster: ClusterDeployment, AgentClusterInstall, InfraEnv.




