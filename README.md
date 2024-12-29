[![CI](https://github.com/de-it-krachten/ansible-role-awx_convert/workflows/CI/badge.svg?event=push)](https://github.com/de-it-krachten/ansible-role-awx_convert/actions?query=workflow%3ACI)


# ansible-role-awx_convert

Convert AWX export into Configuration-as-Code, usable by the role 'awx_import'



## Dependencies

#### Roles
None

#### Collections
None

## Platforms

Supported platforms

- Red Hat Enterprise Linux 8<sup>1</sup>
- Red Hat Enterprise Linux 9<sup>1</sup>
- RockyLinux 8<sup>1</sup>
- RockyLinux 9<sup>1</sup>
- OracleLinux 8
- OracleLinux 9<sup>1</sup>
- AlmaLinux 8<sup>1</sup>
- AlmaLinux 9<sup>1</sup>
- Debian 11 (Bullseye)<sup>1</sup>
- Debian 12 (Bookworm)<sup>1</sup>
- Ubuntu 20.04 LTS<sup>1</sup>
- Ubuntu 22.04 LTS<sup>1</sup>
- Ubuntu 24.04 LTS<sup>1</sup>
- Fedora 41<sup>1</sup>

Note:
<sup>1</sup> : no automated testing is performed on these platforms

## Role Variables
### defaults/main.yml
<pre><code>
# Host to execute code from
awx_delegation_host: localhost

# Should the hosts & groups be extracted from inventory (only for old exports)
awx_extract_from_inventory: false

# List of AWX resources to convert
awx_convert_resources:
  - settings
  - organizations
  - credential_types
  - credentials
  # - execution_environments
  - inventory
  - inventory_sources
  - job_templates
  - notification_templates
  - projects
  - teams
  - users
  - workflow_job_templates
  # - roles  ## Not yet implemented
  - schedules
  # - applications  ## Not yet implemented
  # - system_job_templates  ## Not yet implemented
  - groups
  - hosts

# Dict of additional variable files
awx_convert_vars:
  credential_types:
    - injectors
    - inputs
  groups:
    - variables
  hosts:
    - variables
  inventory:
    - variables
  inventory_sources:
    - source_vars
  job_templates:
    - extra_vars
  schedules:
    - extra_data
  workflow_job_templates:
    - extra_vars
</pre></code>




## Example Playbook
### molecule/default/converge.yml
<pre><code>
- name: sample playbook for role 'awx_convert' pre playbook
  ansible.builtin.import_playbook: converge-pre.yml
  when: molecule_converge_pre is undefined or molecule_converge_pre | bool
- name: sample playbook for role 'awx_convert'
  hosts: all
  become: 'no'
  vars:
    awx_export_path: /tmp/awx
    awx_config_path: /tmp/awx1
  tasks:
    - name: Include role 'awx_convert'
      ansible.builtin.include_role:
        name: awx_convert
</pre></code>
