# Kibana

Install Kibana on a single node. The defaults are fine for a Kibana interface
to a local ES instance.

## Requirements

* Ubuntu 16.04 or Centos 7 on the target host

## Role Variables

### `kibana_server_port`

- TCP port to listen on.
- Default value: **5601**

### `kibana_server_host`

- IPv4 address to bind to. An FQDN will work too.
- Default value: **0.0.0.0**

### `kibana_elasticsearch_url`

- The URL of the Elasticsearch instance Kibana should send queries to.
- Default value: **http://localhost:9200**

### `es_major_version`

- Major version of the ES repo to pull the Kibana packages from.
- Default value: **5.x**

### `es_yum_repo`

- The URL of the repository for Kibana RPM's.
- Default value: **https://artifacts.elastic.co/packages/{{ es_major_version }}/yum**

### `es_yum_gpg`

- The URL for the GPG key that signed the packages in `es_yum_repo`.
- Default value: **https://artifacts.elastic.co/GPG-KEY-elasticsearch**

### `es_apt_repo`

- The URL of the repository for Kibana DEB's.
- Default value: **deb https://artifacts.elastic.co/packages/{{ es_major_version }}/apt stable main**

### `es_apt_gpg`

- The URL for the GPG key that signed the packages in `es_apt_repo`.
- Default value: **{{ es_yum_gpg }}**

## Example Playbook

Sample inventory:

```
[elasticsearch]
192.168.0.42 es_foo=bar
192.168.0.43es_foo=quux

[kibana]
192.168.0.42 kibana_server_host=192.168.0.42
192.168.0.43 kibana_server_host=192.168.0.43
```

and corresponding playbook:

```
- hosts: kibana
  become: yes
  roles:
    - ansible-role-kibana
```

### Vagrant and tests

Cd into `tests/xenial/` and `vagrant up` for an instance of Kibana. You
can also choose to cd into `tests/centos-7` and do the same.

It's not very useful, as there is no ES to connect to.

## License

MIT / BSD

## Maintainer

[Spyridon Gouliarmis](mailto:spyridon.gouliarmis@data-essential.com)

This role was created in 2014 by [Jeff Geerling](https://www.jeffgeerling.com/), author of [Ansible for DevOps](https://www.ansiblefordevops.com/).
