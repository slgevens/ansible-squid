Role Name
=========

Installs squid proxy (Configurable and cache peering, haproxy, keepalived ready)

Requirements
------------

If you want to use haproxy and/or keepalived you will need to install the roles under dependencies and configure each role.
Each role (haproxy, keepalived and squid) should be configured using group_vars/group and host_vars/host. Ensure correct configurations within each role. If you only require squid then you may disregard the haproxy and keepalived roles.

Role Variables
--------------

````
enable_haproxy: false  #defines if haproxy should be installed...define here or in group_vars/group
enable_keepalived: false  #defines if keepalived should be installed...define here or in group_vars/group
haproxy_squid_http_port: 8080  #define load balanced port for clients to connect to if haproxy is used
keepalived_vip: [] #defines keepalived vip if keepalived is used...define here or in group_vars/group
pri_domain_name: example.org  #define primary domain name...define here or in group_vars/all
squid_acl_localnet: [] #defines local subnets to allow to connect to squid...define here or in group_vars/group
#  - 10.0.0.0/8
#  - 172.16.0.0/16
#  - 192.168.0.0/16
squid_cache_peer: [] #defines squid peers to sync with...define here or in group_vars/group #do not enter FQDN...It will be added
#  - host: squid-1  #do not enter FQDN...hostname only
#    domain: '{{ pri_domain_name }}'  #enter domain name for hostname above
#    type: sibling
#    proxy_port: '{{ squid_http_port }}'
#    icp_port: '{{ squid_icp_port }}'
#    options: default
#  - host: squid-2  #do not enter FQDN...hostname only
#    domain: '{{ pri_domain_name }}'  #enter domain name for hostname abov
#    type: sibling
#    proxy_port: '{{ squid_http_port }}'
#    icp_port: '{{ squid_icp_port }}'
#    options: default
squid_cache_peering: false  #define here or in group_vars/group
squid_http_port: 3128  #define here or in group_vars/group
squid_icp_access: all  #define here or in group_vars/group
squid_icp_port: 3130  #define here or in group_vars/group
squid_servers: []  #defines squid servers to configure haproxy if used
#  - squid-1
#  - squid-2
squid_transparent_proxy: false  #defines if squid should function in transparent mode...define here or in group_vars/group
````

Dependencies
------------

````
mrlesmithjr.haproxy
mrlesmithjr.keepalived
````

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: mrlesmithjr.haproxy, when: enable_haproxy }
         - { role: mrlesmithjr.keepalived, when: enable_keepalived }
         - { role: mrlesmithjr.squid }

License
-------

BSD

Author Information
------------------

Larry Smith Jr.
- @mrlesmithjr
- http://everythingshouldbevirtual.com
- mrlesmithjr [at] gmail.com
