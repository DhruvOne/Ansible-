# Nginx Role

Installs and configures Nginx web server with templated configuration.

## What it does
- Installs nginx via the OS package manager
- Deploys a templated site configuration
- Deploys a dynamic index page showing server info
- Starts and enables the nginx service
- Uses handlers to reload on config changes

## Variables

| Variable | Default | Description |
|----------|---------|-------------|
| `nginx_listen_port` | `80` | Port nginx listens on |
| `nginx_server_name` | `_` | Server name (default catch-all) |
| `nginx_root` | `/var/www/html` | Document root |

## Usage

```yaml
- hosts: ubuntu
  roles:
    - role: nginx
      nginx_listen_port: 8080
```
