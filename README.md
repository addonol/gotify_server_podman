# Ansible Role: gotify_server_podman

[![Ansible Galaxy](https://img.shields.io/badge/galaxy-addonol.gotify_server_podman-blue.svg)](https://galaxy.ansible.com/addonol/gotify_server_podman)
[![License: MIT](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)

Deploy [Gotify Server](https://gotify.net/) using [Podman](https://podman.io/) with Ansible.  
This role automates the build, deployment, management, and cleanup of a Gotify notification server containerized with Podman.

---

## Features

- **Automated build** of a custom Gotify server image using Podman.
- **Secure admin password** generation and storage using Podman secrets.
- **Configurable deployment** (port, timezone, data volume, etc.).
- **Lifecycle management**: start, stop, restart, and clean up Gotify server resources.
- **Idempotent and robust**: handles existing resources gracefully.

---

## Requirements

- **Ansible**: `>=2.18.0`
- **Podman** and the [Ansible Podman Collection](https://docs.ansible.com/ansible/latest/collections/containers/podman/index.html) must be available on the target host.

Supported platforms:
- Ubuntu (all versions)

---

## Role Variables

The following variables can be set to customize the role’s behavior (see `defaults/main.yml`):

| Variable                               | Default Value                      | Description                                 |
|----------------------------------------|------------------------------------|---------------------------------------------|
| `gotify_server_podman_image`           | `docker.io/gotify/server:latest`   | Base Gotify image to use                    |
| `gotify_server_podman_custom_image`    | `custom/gotify-server:latest`      | Name for the custom-built image             |
| `gotify_server_podman_build_dir`       | `/tmp/gotify_server_build`         | Build context directory                     |
| `gotify_server_podman_admin_user`      | `admin`                            | Gotify admin username                       |
| `gotify_server_podman_binary_path`     | `/app/gotify-app`                  | Path to Gotify binary in the container      |
| `gotify_server_podman_port_number`     | `8080`                             | Host port for Gotify                        |
| `gotify_server_podman_timezone`        | `Europe/Brussels`                  | Timezone for the container                  |
| `gotify_server_podman_data_dir`        | `/opt/gotify_server_data`          | Data directory on the host                  |
| `gotify_server_podman_volume_name`     | `gotify_server_data`               | Podman volume name                          |
| `gotify_server_podman_container_name`  | `gotify-server`                    | Name of the Gotify container                |

---

## Dependencies

None.

---

## Usage

### Example Playbook

```
hosts: servers
roles:
    - role: addonol.gotify_server_podman
```


### Tags

- `build`: Build and deploy the Gotify server
- `clean`: Remove all Gotify server resources
- `restart`: Restart the Gotify container
- `stop`: Stop the Gotify container

---

## Tasks Overview

- **build.yml**:  
  - Generates a secure admin password (stored as a Podman secret)
  - Removes any existing container, secret, or volume
  - Builds a custom Gotify image from templates
  - Runs the Gotify container with proper environment, secrets, and volume
  - Displays the generated admin password

- **clean.yml**:  
  - Removes the Gotify container, secrets, volumes, and images

- **restart.yml**:  
  - Restarts the Gotify container

- **stop.yml**:  
  - Stops the Gotify container

---

## Example Output

After deployment, the admin password will be displayed in the Ansible output:

```
Gotify Server admin password: <generated_password>
```

---

## License

MIT

---

## Author

[addonol](https://galaxy.ansible.com/addonol)

---

## Galaxy Metadata

- **Namespace:** addonol
- **Role Name:** gotify_server_podman
- **Minimum Ansible Version:** 2.18.0
- **Platforms:** Ubuntu (all versions)

