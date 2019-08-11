# Ansible role for Drone.io server

This Ansible role installs the drone.io server in a docker container.
The configuration for the server can be specified in your playbook as
shown below:

```
- name: Example drone.io server
  hosts: drone.myorg.org
  become: yes
  roles:
    - role: caddy-git
      tags: caddy
      caddy_config: |
        drone.myorg.org {
          proxy / localhost:8000
        }

    - role: drone-server
      tags: drone
      drone_server_env: |
        DRONE_GITHUB_SERVER=https://github.com
        DRONE_GITHUB_CLIENT_ID=<insert here>
        DRONE_GITHUB_CLIENT_SECRET=<insert here>
        DRONE_AGENTS_ENABLED=true
        DRONE_RPC_SECRET=<insert here>
        DRONE_SERVER_HOST=drone.myorg.org
        DRONE_SERVER_PROTO=https
        DRONE_TLS_AUTOCERT=false
        DRONE_LOGS_DEBUG=true
        DRONE_USER_CREATE=username:cbrake,machine:false,admin:true
        DRONE_USER_FILTER=cbrake,kraj
```

In the above example, we use Caddy as a reverse proxy for the drone server,
which works very well.
