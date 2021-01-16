# Netscaler Upgrade with Ansible

## Environment

* Ansible version: 2.9.1
* Netscaler source version: 12.0 (60.10)
* Netscaler target version: 12.1 (55.18)

## Playbook Execution
```
ansible-playbook nsuri_upgrade.yml
```
![alt text](<images/upgrade.PNG>)

## Version Check
```
ansible-playbook nsmodule_version.yml
```
![alt text](<images/version.PNG>)

## Notes

* I used passwords in cleartext just for completion, don't do this in production (use ansible vault).
