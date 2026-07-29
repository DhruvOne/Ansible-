# Module 6: Ansible Vault

## What you'll learn
- Encrypt and decrypt files using `ansible-vault`
- Load secrets from vault-encrypted variable files
- Hide sensitive output with `no_log: true`

## Prerequisites
- Completed Modules 1–5
- Infrastructure provisioned with Terraform (`cd terraform && terraform apply`)
- Inventory auto-generated at `inventories/dev/hosts.ini`

## Setup (one-time)

```bash
# Create a vault password file (so you don't type it every time)
echo "training" > ~/.vault_pass.txt
chmod 600 ~/.vault_pass.txt

# Encrypt the secrets file
ansible-vault encrypt modules/06-vault/vars/secrets.yml --vault-password-file ~/.vault_pass.txt
```

## Vault Commands (Try these first!)

```bash
# Encrypt a file
ansible-vault encrypt modules/06-vault/vars/secrets.yml

# View encrypted file without decrypting on disk
ansible-vault view modules/06-vault/vars/secrets.yml --vault-password-file ~/.vault_pass.txt

# Edit encrypted file in place
ansible-vault edit modules/06-vault/vars/secrets.yml --vault-password-file ~/.vault_pass.txt

# Decrypt a file (removes encryption)
ansible-vault decrypt modules/06-vault/vars/secrets.yml --vault-password-file ~/.vault_pass.txt
```

## Playbooks in This Module

| # | Playbook | Concepts Taught |
|---|----------|----------------|
| 1 | `01_vault_basics.yml` | vars_files with vault, transparent decryption |
| 2 | `02_no_log.yml` | no_log: true, hiding secrets in output |
| 3 | `03_create_config.yml` | Using vault secrets to create config files |

## How to Run

```bash
# Run from the repo root directory
ansible-playbook modules/06-vault/01_vault_basics.yml --vault-password-file ~/.vault_pass.txt

# Or type the password interactively
ansible-playbook modules/06-vault/02_no_log.yml --ask-vault-pass
```

## Good to know
- **Never commit plaintext secrets** — always encrypt with vault before committing
- Vault encrypts at rest — secrets are decrypted in memory only during playbook runs
- Use `no_log: true` on tasks that handle secrets to prevent them from showing in output
- The `package` module doesn't need vault — vault is only for secrets like passwords and API keys
