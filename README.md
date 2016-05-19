Role Name
=========

Docker container running postgresql.

Requirements
------------

- python >= 2.6
- docker-py >= 0.3.0
- Docker >= 1.9
- Ansible >= 2.1

Role Variables
--------------

`use_datastore_container`: Optional, whether to use a separate container to store postgresql data files. Default true.  
`datastore_container_name`: Optional, the container name to store data. Default 'postgres-datastore'.  
`postgres_container_name`: Optional, the container name where postgresql running in. Default 'postgres'.  
`expose_host_port`: Optional, the port to expose postgresql to the host. Default not expose postgresql to the host.  
`postgres_docker_tag`: Optional, the postgres docker image tag name to use. Default 'latest'.  
`postgres_docker_env`:  Optional, a dict of env var to be passed into postgresql container. Check [postgres docker page](https://hub.docker.com/_/postgres).  


Dependencies
------------


Example Playbook
----------------

    - hosts: servers
      roles:
         - role: username.rolename
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


License
-------

MIT

Author Information
------------------

YoctolInfo
