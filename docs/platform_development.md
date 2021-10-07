# Platform Development

## Requirements
- vagrant + vagrant-libvirt plugin
- libvirtd running
- ansible

## Prepare dev environment
- cd into project root path
- `ansible-galaxy install --role-file ansible_galaxy_requirements.yml`
    - some ansible roles used from ansible galaxy
- `vagrant up --no-provision`
    - creates dev vm
    - without `--no-provision` it would begin to run the ansible scripts and destroy the vm again in case of some error


## Development
### Run the whole ansible playbook
`vagrant provision`

### Run only specific tasks
`ansible-playbook -i .vagrant/provisioners/ansible/inventory/vagrant_ansible_inventory --tags locales playbook.homecloud.yml`

### Ssh into vm
`vagrant ssh`

### Destroy vm
`vagrant destroy`

