wzzrd.atuin_client
=========

Configures atuin client component

The current version of this role does *not* provide functionality to log into an atuin server. It does configure the client for selected users through `config.toml`, but you will have to run `atuin login` on systems yourself after using this role. Future versions of this role might include this functionality as well.

Requirements
------------

It is mandatory to provide a value for the `atuin_client_version` variable.

The role will fail without a value for `atuin_client_version`. This variable is used by the `wzzrd.atuin_client` role to install the atuin binary. It is expected to be a string naming an atuin version: `18.0.1` is a valid value that will make the role succeeed.

Role Variables
--------------

| Variable name | Default value | Meaning | Mandatory |
|---------------|---------------|---------|-----------|
| atuin_client_version | None | Version of atuin to install | true |
| atuin_client_bin_dir | /usr/local/bin | Location for the atuin binary | false |
| atuin_client_libc_variant | gnu | Which libc implementation to download a binary for | false |
| atuin_client_users | None | List of users to create a configuration file for | false |

The `atuin_client_libc_variant` expects one of two options: musl or gnu. Choosing gnu will make the role download the atuin binary compiled for an OS with a recent build of glibc. Choosing musl will download a binary compiled and statically linked to the musl libc implementation. This allows you to run atuin on systems with incompatible versions of glibc.

Mind that the musl build (at the time of writing) is only available for x86_64 Linux. Trying to install that build on aarch64 Linux will not work.

The only resort in that case is to use cargo to install atuin. I might implement that in a future version of this role.

The `atuin_client_users` variable can be used to pass a list of usernames to the role.
The role will iterate over this list and create a configuration file based for each
user. This configuration file is based on the values provided to this role and the
contents of `templates/config.toml.j2`. If the user changes this file, subsequent runs
of this role will *not* overwrite it.

Please see the `defaults/main.yml` file for the other configurable variables, their
default values and an explanation of what they are for.

Dependencies
------------

None

Compatibility
-------------

This role is compatible with EL8 and EL9 systems, and has been automatically tested through molecule on ubi8 and ubi9 container images.

Example Playbook
----------------

This role is used in the following way in a playbook:

```yaml
- hosts: atuin_clients
  vars:
    atuin_client_users:
      - johnc
      - joeb
    atuin_client_version: 18.0.1

  roles:
    - role: wzzrd.atuin.atuin_client
```

License
-------

BSD-3-Clause

Author Information
------------------

This role was created by Maxim Burgerhout <maxim@wzzrd.com> as part fo the wzzrd.atuin Ansible collection.

Please log issues at https://github.com/wzzrd/ansible-collection-atuin.
