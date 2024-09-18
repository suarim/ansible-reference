# ansible adhoc
ansible -i inventory.ini -m "apt" -a "name=nginx state=present" all

# running playbook
ansible-playbook -i inventory.ini playbook.yaml

# using extra variables
ansible-playbook -i inventory.ini playbook.yaml -e '{book:harry}'

# vaults
ansible-vault create group_vars/my_vault.yml

ansible-vault edit group_vars/my_vault.yml

ansible-vault view group_vars/my_vault.yml 

# Vault file - my_vault.yml
ansible-playbook --inventory inventory.ini ansible-vault-playbook.yml -e @group_vars/my_vault.yml --ask-vault-pass

# create encrypted password
openssl rand -base64 2048 > pass_file/ansible-vault.pass

# use encrypted password
ansible-vault create group_vars/my_vault_with_bas64_pass.yml --vault-password-file=pass_file/ansible-vault.pass

# setting password path to environment
export ANSIBLE_VAULT_PASSWORD_FILE=/Users/rahulwagh/Documents/Documents-Rahul-MacBook-Pro/jhooq/ansible-examples/part-14-ansible-vault/pass_file/ansible-vault.pass

# no need for password as password present in environment
ansible-playbook --inventory inventory.ini ansible-vault-playbook.yml -e @group_vars/my_vault_with_bas64_pass.yml

# downloading collections
ansible-galaxy collection install amazon.aws

# initializing role
ansible-galaxy init role_name