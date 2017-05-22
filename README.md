# Burnashev Roman. The test task for the DevOps engineer candidates.

Use:
* Clone this repository on local mashine/
* install ansible
* Start playbook:
ansible-playbook -e "target=hostname" --ask-vault-pass /path/to/repo/mos/main.yml

vault_pass i will post by mail.
if target host not have ssh keys - use -k options for enter root passwd
