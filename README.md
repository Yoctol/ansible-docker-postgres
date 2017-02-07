Role Name
=========

Docker container running postgresql.

Requirements
------------

- python >= 2.6
- docker-py >= 1.7.0
- Docker API >= 1.20
- Ansible >= 2.2

Role Variables
--------------

```yaml
---
# Optional, whether to use a separate container to store postgresql data files.
# Default true.
use_datastore_container: true

# Optional, the container name to store data. Default 'postgres-datastore'.
datastore_container_name: postgres-datastore

# Optional, the postgres docker image tag name to use. Default 'latest'.
postgres_docker_tag: ''

# Optional, the container name where postgresql running in. Default 'postgres'.
postgres_container_name: postgres

# Optional, a dict of env var to be passed into postgresql container.
# Check [postgres docker page](https://hub.docker.com/_/postgres).
postgres_docker_env: []

# Optional, the port to expose postgresql to the host.
# Default not expose postgresql to the host.
expose_host_port: 0
```

Dependencies
------------


Example Playbook
----------------

```yaml
- hosts: servers
  roles:
    - role: ansible-docker-postgres
      use_datastore_container: true
      datastore_container_name: dbstore
      postgres_container_name: postgres
      expose_host_port: 5432
      postgres_docker_tag: 9.5
      postgres_docker_env:
        POSTGRES_PASSWORD: pg_admin_pw
        POSTGRES_USER: pg_admin_user
        PGDATA: /var/lib/postgresql/data/pgdata
        POSTGRES_DB: pg_default_db
        POSTGRES_INITDB_ARGS: "--data-checksums"

# The address of container is set to the fact `postgres_container_address`.
# You can use it to connect postgres server.
- postgres_user:
    name: foo
    login_user: postgres
    login_host: "{{ postgres_container_address }}"
```

License
-------

MIT

Author Information
------------------

YoctolInfo Inc.
