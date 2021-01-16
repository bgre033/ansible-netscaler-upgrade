# Netscaler Upgrade with Ansible

## Environment

* Ansible version: 2.9.1
* Netscaler source version: 12.0 (60.10)
* Netscaler target version: 12.1 (55.18)

## Playbook - Upgrade

* The upgrade playbook uses the default Ansible URI module to call Netscaler's API, https://docs.ansible.com/ansible/latest/collections/ansible/builtin/uri_module.html.
* The version check playbook uses Netscaler Nitro Request plugin from the Ansible Community Network collection (https://docs.ansible.com/ansible/latest/collections/community/network/, https://github.com/ansible-collections/community.network)
* Modify 'ns_upgrade_vars.yml' as required. I set the upgrade path (ns_binary_url) to a local file on the NetScaler (to speed up the process), but you can also instruct the NetScaler to download the file from another location.
* I used passwords in cleartext just for completion, don't do this in production (use Ansible vault).
* Setting the reboot paramter (y) to 'true', causes the playbook to fail, hence the playbook executes two separate tasks. First it performs the upgrade, and based on the output of the upgrade task (200, 201), it executes a reboot task.
* If your playbook fails or is intermittent, try setting TCP client keepalives (http://coryklein.com/tcp/2015/11/25/custom-configuration-of-tcp-socket-keep-alive-timeouts.html), as this is currently not configurable from the NetScaler. Citrix have two enhancemets logged for this feature (NSNET-15877 & NSNET-15878).

```
ansible-playbook nsuri_upgrade.yml
```
![alt text](<images/upgrade.PNG>)

## Playbook - Version Check
```
ansible-playbook nsmodule_version.yml
```
![alt text](<images/version.PNG>)
test