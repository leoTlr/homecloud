# Service development

1. [Install platform with ansible](./platform_development.md)
    - use vagrant testenv or deploy on debian 11 host
    - put settings in `settings_{dev,prod}.yml`
2. Define Service in `playbook.homecloud.services.yml`
    - use ansible role service_template
        - [vars](../roles/service_template/defaults/main.yml)
    - creates an Ingress for `<app_name>.<platform_fqdn>`
        - for testenv add `192.168.60.2    homecloud.test webtest.homecloud.test` to  `/etc/hosts`
3. Deploy service with ansible
    - `ansible-playbook -i .vagrant/provisioners/ansible/inventory/vagrant_ansible_inventory playbook.homecloud.services.yml --extra-vars "env=dev"`

## Example Service
```Yaml
- name: install example service
  become: True
  hosts: homecloud
  tags:
    - service
    - service_web
  roles:
    - service_template
  vars_files:
    - 'settings_{{ env }}.yml'
  vars:
    app_name: webtest
    app_state: present
    app_port: 8080
    host_port: 80
    persistence_enabled: false
    container_image: paulbouwer/hello-kubernetes:1.5
```
