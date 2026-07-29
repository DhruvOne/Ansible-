# Module 3: Templates and Handlers

## What you'll learn
- Write Jinja2 templates using Ansible facts and variables
- Deploy configuration files with the `template` module
- Understand the difference between `copy` and `template`
- Use handlers to restart services only when configuration changes
- Learn handler deduplication and `notify`

## Playbooks in This Module

| # | Playbook | Concepts Taught |
|---|----------|----------------|
| 1 | `01_deploy_nginx_config.yml` | template module, notify, handlers |
| 2 | `02_motd_template.yml` | Jinja2 expressions, facts in templates |
| 3 | `03_handlers_demo.yml` | Handler deduplication, multiple notifies |

## Templates

| Template | Purpose |
|----------|---------|
| `templates/nginx.conf.j2` | Nginx config with variables and facts |
| `templates/index.html.j2` | Dynamic landing page with server info |
| `templates/motd.j2` | Message of the Day with system info |

## How to Run

```bash
ansible-playbook modules/03-templates-and-handlers/01_deploy_nginx_config.yml
ansible-playbook modules/03-templates-and-handlers/02_motd_template.yml

# Run twice — notice the handler only fires on the first run!
ansible-playbook modules/03-templates-and-handlers/03_handlers_demo.yml
ansible-playbook modules/03-templates-and-handlers/03_handlers_demo.yml
```

## Good to know
- `template` renders Jinja2 on the control node, then copies the result to the target
- `copy` sends a static file as-is — no variable substitution
- Handlers run **once** at the end of the play, even if notified multiple times
- Handlers only run if the notifying task **changed** something
- Use handlers to restart services — avoids unnecessary restarts
