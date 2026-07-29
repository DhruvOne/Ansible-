# Module 5: Roles

## What you'll learn
- Ansible role directory structure
- Creating roles with `ansible-galaxy init`
- Using `defaults`, `tasks`, `handlers`, `templates` in roles
- Applying roles in playbooks
- Writing a `site.yml` that brings it all together

## What is a Role?

Instead of writing one giant playbook, you split your automation into roles — like `common`, `docker`, `nginx`. Each role handles one thing.

### Role Directory Structure
```
roles/
└── docker/
    ├── defaults/main.yml     # Default variables (lowest priority)
    ├── tasks/main.yml        # Main task list
    ├── handlers/main.yml     # Handlers (e.g., restart service)
    ├── templates/            # Jinja2 templates
    ├── files/                # Static files
    ├── meta/main.yml         # Role metadata and dependencies
    └── README.md             # Documentation
```

### Creating a New Role
```bash
# Use ansible-galaxy to scaffold a new role
ansible-galaxy init roles/my_new_role

# This creates the full directory structure automatically
```

## Roles in This Repo

| Role | Purpose | Path |
|------|---------|------|
| `common` | Base setup: packages, timezone, MOTD | `roles/common/` |
| `docker` | Docker install across Ubuntu/RHEL/Amazon | `roles/docker/` |
| `nginx` | Nginx with templated config and handlers | `roles/nginx/` |

## Playbooks in This Module

| Playbook | Description |
|----------|-------------|
| `site.yml` | Master playbook — applies all roles to appropriate hosts |

## How to Run

```bash
# Apply everything
ansible-playbook modules/05-roles/site.yml

# Apply to specific hosts only
ansible-playbook modules/05-roles/site.yml --limit ubuntu
```

## Good to know
- `defaults/main.yml` variables can be overridden by inventory, playbook, or `-e` on the CLI
- Handlers in roles are global — watch out for naming conflicts
- `site.yml` is the standard name for a master playbook
