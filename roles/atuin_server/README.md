wzzrd.atuin_server
=========

Configures atuin server component

Requirements
------------

It is mandatory to provide values for the `atuin_client_version` and `atuin_server_db_uri` variables.

The role will fail without a value for `atuin_client_version`. This variable is used by the `wzzrd.atuin_client` role to install the atuin binary. It is expected to be a string naming an atuin version: `18.0.1` is a valid value that will make the role succeeed.

The role will succeed, and the atuin server process will start without `atuin_server_db_uri` but will not be fully functional. It expects a PostgreSQL connection URI in the form `postgres://user:password@server/database`.

Role Variables
--------------

| Variable name | Default value | Meaning | Mandatory |
|---------------|---------------|---------|-----------|
| atuin_client_version | None | Version of atuin to install | true |
| atuin_server_db_uri | None | PostgreSQL database connection URI (see below) | true |
| atuin_server_user | atuin | The name of the user owning the atuin server process | false |
| atuin_server_group | atuin | The name of the group owning the atuin server process | false |
| atuin_server_home | /home/atuin | The home directory for the atuin server user | false |
| atuin_server_host | "{{ ansible_default_ipv4.address }}" | IP address the atuin server process will listen on | false |
| atuin_server_port | 8888 | The port the atuin server process will listen on | false |
| atuin_server_open_registration | false | Whether or not the server will freely allow registration | false |
| atuin_server_max_history_length | 8192 | Maximum length of one history entry | false |
| atuin_server_max_record_size | 1073741824 | Maximum length of one record entry | false |
| atuin_server_page_size | 1100 | Default page size for requests | false |
| atuin_server_enable_metrics | false | Whether metrics are enabled | false |
| atuin_server_metrics_host | 127.0.0.1 | IP address for the metrics process | false |
| atuin_server_metrics_port | 9001 | Port for the metrics process | false |
| atuin_server_enable_tls | false | Whether or not to use TLS for the atuin server process | false |
| atuin_server_cert_path | "" | Path to an SSL certificate | false |
| atuin_server_pkey_path | "" | Path to the SSL certificate private key | false |

Dependencies
------------

This role depends on the `wzzrd.atuin_client role`, distributed in the same collection. The `atuin_client` role handles the download of the correct binary (and possibly upgrading an existing binary), the `atuin_server` role handles the server configuration, the systemd unit file, and the ownership of the atuin server process.

Compatibility
-------------

This role is compatible with EL8 and EL9 systems, and has been automatically tested through molecule on ubi8 and ubi9 container images.


Example Playbook
----------------

This role is used in the following way in a playbook:

```yaml
- hosts: atuin_server
  vars:
    atuin_client_version: 18.0.1
    atuin_server_db_uri: "postgres://atuin:atuinpw@dbserver/atuindb"

  roles:
    - role: wzzrd.atuin.atuin_server
```

License
-------

BSD-3-Clause

Author Information
------------------

This role was created by Maxim Burgerhout <maxim@wzzrd.com> as part fo the wzzrd.atuin Ansible collection.

Please log issues at https://github.com/wzzrd/ansible-collection-atuin.