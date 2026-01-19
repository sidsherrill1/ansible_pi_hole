# Ansible Pi-hole Project

This Ansible project automates the deployment and configuration of Pi-hole DNS servers across two virtual machines.

## Project Structure

```
ansible_pi-hole_AI-agent/
├── ansible.cfg              # Ansible configuration
├── inventory/               # Inventory files
│   └── hosts.ini           # Host definitions for Pi-hole VMs
├── playbooks/              # Ansible playbooks
│   └── setup_pihole.yml    # Main playbook for Pi-hole setup
├── roles/                  # Ansible roles
│   └── pihole/             # Pi-hole role
│       ├── tasks/          # Role tasks
│       ├── handlers/       # Event handlers
│       ├── templates/      # Template files
│       ├── files/          # Static files
│       ├── vars/           # Role variables
│       └── defaults/       # Default variables
├── group_vars/             # Group variables
│   └── pihole_vms.yml      # Variables for all Pi-hole VMs
├── host_vars/              # Host-specific variables
│   ├── pihole-vm-1.yml     # Variables for VM-1
│   └── pihole-vm-2.yml     # Variables for VM-2
└── README.md               # Project documentation
```

## Getting Started

### Prerequisites
- Ansible 2.9+
- SSH access to both Pi-hole VMs
- Python 3 installed on target hosts

### Configuration

1. Update inventory IP addresses in `inventory/hosts.ini`:
   ```ini
   pihole-vm-1 ansible_host=<actual-ip-1>
   pihole-vm-2 ansible_host=<actual-ip-2>
   ```

2. Configure host-specific variables in `host_vars/`:
   - Update upstream DNS servers
   - Set admin passwords securely

3. Set up SSH key authentication for passwordless access

### Running the Playbook

```bash
# Run the Pi-hole setup playbook
ansible-playbook playbooks/setup_pihole.yml

# Run for a specific host
ansible-playbook playbooks/setup_pihole.yml -l pihole-vm-1

# Verify connectivity
ansible all -i inventory/hosts.ini -m ping
```

## Security Considerations

- Use Ansible Vault for sensitive data (passwords)
- Store SSH keys securely
- Restrict access to inventory files
- Use strong admin passwords for Pi-hole

## Vault Setup (Optional)

```bash
# Create a vault for sensitive variables
ansible-vault create group_vars/pihole_vms_vault.yml

# Edit vault
ansible-vault edit group_vars/pihole_vms_vault.yml

# Run playbook with vault
ansible-playbook playbooks/setup_pihole.yml --ask-vault-pass
```

## Next Steps

1. Add more roles (e.g., monitoring, backup)
2. Create maintenance playbooks
3. Implement health checks
4. Add configuration management for adlists
