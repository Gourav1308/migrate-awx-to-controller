# ACM-EDA
# High Level steps


. Packages required
   ```
$  python3 -m pip install ansible-navigator>=3.4.2 --user
$  python3 -m pip install ansible-builder>=3.0.0 --user
   ```

. Run the playbook to export the configuration in the automation controller:
   ```
   ansible-navigator run playbooks/config-controller-export.yaml -i localhost -m stdout --eei quay.io/automationiberia/casc/ee-casc:latest --eev /tmp/:/tmp/ -e @vars/vault.yaml --vault-password-file .vault-password  -e'{ansible_async_dir: /home/runner/.ansible_async/}'
   ```
. Run the playbook to apply the configuration in the automation controller:
   ```
    ansible-navigator run playbooks/config-controller-filetree.yaml -i localhost -m stdout --eei quay.io/automationiberia/casc/ee-casc:latest --vault-password-file .vault-password -e @vars/vault.yaml -e @vars/controller.yaml -e @vars/paths.yaml --vault-password-file .vault-password -e'{controller_configuration_filetree_read_secure_logging: false,ansible_async_dir: /home/runner/.ansible_async/}'
   ```

. Run the playbook to apply the configuration in the automation eda:
   ```
    ansible-navigator run playbooks/config-eda.yaml -i localhost -m stdout --eei quay.io/automationiberia/casc/ee-casc:latest --eev /tmp/:/tmp/ -e @vars/vault.yaml --vault-password-file .vault-password  -e'{ansible_async_dir: /home/runner/.ansible_async/}
   ```
