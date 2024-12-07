Ansible Role: Subsonic-docker
=============================

Install Subsonic Docker Compose project.

- https://www.subsonic.org/

Requirements
------------

Requires the following to be installed:
- docker
- docker compose

Role Variables
--------------

Common Docker projects variables:

```yaml
# Base directory for Docker projects
docker_projects_path: # /var/apps
```

Available role variables are listed below, along with default values (see `defaults/main.yml`):

```yaml
# Docker project variables

subsonic_project_name: subsonic

# Docker project dynamic vars (uses `docker_project_name` prefix, adapt if overriden)

subsonic_traefik_loadbalancer_server_port: 4040
subsonic_traefik_entrypoints: http,https
subsonic_traefik_middlewares:
  - "https-redirect@file"
  - "rewrite-location-https@file"

# Main service additional docker-compose options (ex: cpu_shares, deploy, ...)
subsonic_compose_service_additional_options: |
  #ports:
  #  - "4040:4040"
```

```yaml
# stuckj/subsonic container version
subsonic_version: latest

# Media directories
subsonic_media_volumes: []
#  - src: /var/music
#  - src: /var/podcasts
```

Dependencies
------------

This role depends on :
- [djuuu.docker_project](https://github.com/Djuuu/ansible-role-docker-project)

Some variables allow integration with:
- [djuuu.traefik_docker](https://github.com/Djuuu/ansible-role-traefik-docker)

Example Playbook
----------------

```yaml
- hosts: all
  gather_facts: true
  gather_subset:
    - "!all"
    - "!min"
    - user_id

  roles:
    - djuuu.subsonic_docker
```

License
-------

Beerware License
