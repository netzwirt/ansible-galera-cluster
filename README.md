#galera-cluster

##Features

- Setup mariadb galera cluster. 
- Bootstrap new master and slaves.
- Install percona xtradb scripts and services. (@see https://github.com/olafz/percona-clustercheck)

#Role Variables

##Passwords

Passwords have to be stored on local ansible machine.

Set the path for the storage with `galera_password_lookup_dir`

##Group vars

`galera_server_package`: mariadb-server-10.1

`galera_cluster_name`: galera

`galera_bind_address`: 0.0.0.0

`galera_manage_users`: True

It is mandatory, that you keep the galera_cluster_name the same as your group_var name, otherwise you will get errors.

##Host vars


Set `galera_bootstrap` to True on one node, this will be the initial master node.

Set `galera_node_ip` for each host (@see example inventory)


##Monitor cluster via http
@see https://github.com/olafz/percona-clustercheck

Set `galera_check_scripts` to True if you like to install the percona clustercheck scripts

Set port for the xinetd service `galera_check_scripts_port`


##Checkuser for haproxy

Create a checkuser for HAproxy with no password:

Enable `galera_haproxy_user`-> True.

List all allowed hosts in `galera_haproxy_hosts`


##Install perconas nagios plugins

Run playbook with:

	--tags=nagios-plugins --extra-vars="{galera_nagios_plugins_version: '1.1.6'}"

Plugins will be installed in /usr/lib/nagios/percona-plugins/ and copied to 


#Dependencies

None

#Example


##Inventory

    [galera]
    aav.gluster01 galera_node_ip=10.100.2.91 
    aav.gluster02 galera_node_ip=10.100.2.92 galera_bootstrap=1
    aav.gluster03 galera_node_ip=10.100.2.93 

##Playbook

     - hosts: galera
       become: true
       roles:
         - netzwirt.galera-cluster


#License

BSD

#Author Information

[netzwirt](https://github.com/netzwirt)

