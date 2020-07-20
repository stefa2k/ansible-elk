# ansible-elk

[Ansible](https://www.ansible.com/) playbook to set up and maintain [ELK](https://www.elastic.co/what-is/elk-stack) either as stand-alone or cluster.

## Requirements on the host(s)
* Linux with apt
* [Docker](https://www.docker.com/) & [docker-compose](https://docs.docker.com/compose/)

## Configuration
### Common variables
Variable | Description
---------|-------------
`elk_user` | User to run elk with
`elk_install_path` | Path of elk installation
`logstash_custom_filters` | Custom filters for logstash
`index_template_files` | JSON files to import index templates (Elasticsearch)
`dashboard_files` | JSON files to import dashboards (Kibana)

### Host variables
This variables customize the setup [on each host separately](https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html#assigning-a-variable-to-one-machine-host-variables).

Variable | Description | Mandatory
---------|-------------|----------
`elk_listen_ip` | IP to listen on | Yes
`kibana_enabled` | Run Kibana on this host | Yes
`logstash_enabled` | Run Logstash on this host | Yes
`elk_node_init_master` | Initial setup master nodes (should never change after initial setup) | Yes
`elk_node_master` | Run this Elasticsearch node as master | No (default `yes`)
`elk_node_data` | Run this Elasticsearch node as data | No (default `yes`)

## Run
Example:
```
ansible-playbook -i inventory.yaml -l node1,node2,node3 elk.yaml
```
