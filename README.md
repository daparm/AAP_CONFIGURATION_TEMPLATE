# Ansible Automation Platform Configuration as Code examples template

This is a combination of all the Red Hat CoP Config as Code collections to deploy and configure AAP. This is built for multi environment (meaning multiple AAP instances/clusters). If you want an object across all environments put it in the correct file/list under the all group. If there is a specific object for only one environment then put it under that environments folder[^1].

[^1]: If you only have/want one environment you could delete dev/test/prod folders in group_vars and remove all the _all added to vars in all group. Also if you want to have each team/group maintain their own org/code in their own repo, see the repo_per_org branch.

You will need to replace the vault files with your own with these variables:

```yaml
---
cloud_token: 'this is the one from console.redhat.com'
offline_token: 'this is the one linked below about api token'
rh_username: 'redhat user login (this is used to attach your subs to controller)'
rh_password: 'password for redhat account'
root_machine_pass: 'password for root user on builder (if not root user more changes will need to be made)'
ah_token_password: 'this will create and use this password can be generated'
controller_api_user_pass: 'this will create and use this password can be generated'
controller_pass: 'admin account pass for controller, if none is given it will default to Password1234!'
ah_pass: 'hub admin account pass, if none is given it will default to Password1234!'
vault_pass: 'the password to decrypt this vault'
...
```

**_NOTE:_** Do not forget to update your inventory files replacing the `HERE` lines, if you do not have a `builder` server you can use `hub` for this. Also update `scm_url` in `group_vars/all/projects.yml` with your git URL.

## Getting Help

We are on the Ansible Forums and Matrix, if you want to discuss something, ask for help, or participate in the community, please use the #infra-config-as-code tag on the fourm, or post to the chat in Matrix.

[Ansible Forums](https://forum.ansible.com/tag/infra-config-as-code)

[Matrix Chat Room](https://matrix.to/#/#aap_config_as_code:ansible.com)

## Requirements

The awx.awx or ansible.controller collections MUST be installed in order for this collection to work. It is recommended they be invoked in the playbook in the following way.

```yaml
---
- name: Playbook to configure ansible controller post installation
  hosts: localhost
  connection: local
  vars:
    aap_validate_certs: false
  collections:
    - awx.awx
```

## Links to Ansible Automation Platform Collections

|                                      Collection Name                                         |                 Purpose                  |
|:--------------------------------------------------------------------------------------------:|:----------------------------------------:|
| [awx.awx/Ansible.controller repo](https://github.com/ansible/awx/tree/devel/awx_collection) |   Automation controller modules          |
|        [Ansible Hub Configuration](https://github.com/ansible/automation_hub_collection)     |       Automation hub configuration       |

## Links to other Validated Configuration Collections for Ansible Automation Platform

|                                      Collection Name                                       |                 Purpose                  |
|:------------------------------------------------------------------------------------------:|:----------------------------------------:|
| [Controller Configuration](https://github.com/redhat-cop/controller_configuration) |   Automation controller configuration    |
|             [EE Utilities](https://github.com/redhat-cop/ee_utilities)             | Execution Environment creation utilities |
|     [AAP installation Utilities](https://github.com/redhat-cop/aap_utilities)      |  Ansible Automation Platform Utilities   |
|   [AAP Configuration Template](https://github.com/redhat-cop/aap_configuration_template)   |  Configuration Template for this suite   |


## aap config

`ansible-playbook -i inventory_test.yml -l test playbooks/aap_config.yml`
`ansible-playbook -i inventory_test.yml -l test playbooks/aap_config_eda.yml`

## custom ee

currently doesn't work in CLI, expected to be run in Controller

## custom collections

currently doesn't work in CLI, expected to be run in Controller

## aap utilities (aap installer)

`ansible-playbook -i inventory_test.yml -l test playbooks/install_aap.yml`

Acquire your token at [redhat api](https://access.redhat.com/management/api/) see [access article](https://access.redhat.com/articles/3626371)

## install and configure

`ansible-playbook -i inventory_test.yml -l test playbooks/install_configure.yml`

Acquire your token at [redhat api](https://access.redhat.com/management/api/) see [access article](https://access.redhat.com/articles/3626371)


## Open Issues:

Task:
infra.aap_configuration.hub_collection : Update or destroy Automation Hub Collection

takes to long => temporary commented out variable_set "hub_collections"



Trigger EDA Endpoint:

curl -H 'Content-Type: application/json' -d "{\"message\": \"Ansible is alright\"}" 127.0.0.1:5000/endpoint


## Progress:

ansible-playbook -i inventory_test.yml -l test playbooks/aap_config.yml

Run: (25)
gateway_users
gateway_applications
gateway_organizations
gateway_teams
gateway_users
hub_namespace
hub_collection_remote
hub_collection_repository
hub_collection_repository_sync
controller_settings
controller_organizations
controller_labels
controller_credential_types
controller_credentials
controller_execution_environments
controller_projects
controller_inventories
controller_inventory_sources
controller_inventory_source_update
controller_job_templates
controller_schedules
eda_credentials
eda_projects
eda_decision_environments
eda_rulebook_activations

Skipped: (30)
gateway_authenticators
gateway_authenticator_maps
gateway_settings
gateway_http_ports
gateway_service_clusters
gateway_service_keys
gateway_service_nodes
gateway_services
gateway_role_user_assignments
gateway_routes
hub_collection
hub_ee_repository_sync
controller_instances
controller_bulk_host_create
controller_job_launch
controller_workflow_launch
hub_ee_registry
hub_ee_repository
hub_ee_image
hub_ee_registry
hub_ee_registry_index
hub_ee_registry_sync
controller_instance_groups
controller_credential_input_sources
controller_applications
controller_notification_templates
controller_hosts
controller_host_groups
controller_workflow_job_templates
eda_controller_tokens











