# ansible-role-openldap

This role is based on this one: https://github.com/CESNET/ansible-role-ldap-perun


it helps you to install and configure the latest version OpenLDAP from the Debian (currently this is the only tested plateforme) repository.


## Requirements

None.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`).

Domain related to this OpenLDAP install - we also use this value to generate our base DN (For more information see slapd_basedn variable):
    slapd_domain: 'example.net'


Base DN for our OpenLDAP installation, by default we will use the domain to generate it:
    slapd_basedn: '{{ "dc=" + slapd_domain.split(".") | join(",dc=") }}'


Admin user for our data tree
    slapd_basedn_admin: '{{ "cn=admin," + slapd_basedn }}'
    organization: 'example'


Password for the user of our data tree
    ldap_data_tree_password: 'test'


Password for the cn=config tree, by default we reuse the password of the data tree (please don't do that in production):
    config_admin_password: '{{ ldap_data_tree_password }}'


Certificates and key files related to our OpenLDAP install. Those file must be generated before using this role:
    ldap_certificate_file: '/etc/ssl/certs/ssl-cert-snakeoil.pem'
    ldap_certificate_key_file: '/etc/ssl/private/ssl-cert-snakeoil.key'
    ldap_ca_certificate_file: '/etc/ssl/certs/ssl-cert-snakeoil.pem'

## Example Playbook

    - hosts: server
      roles:
        - { role: l00ptr.openldap }

## License

MIT / BSD

## Author Information

This role was created in 2019 by [Jan Pavlíček](https://github.com/xpavlic) and forked by [Julian Vanden Broeck](https://github.com/l00ptr) in 2021.
