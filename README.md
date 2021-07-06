# ansible-role-hashicorp_vault

This role will install Hashicorp Vault via download.

It will download the version specified in var: vault_version, this is currently set to 1.7.2. Changing this value will replace the currently installed version with the one specified. So it is possible to upgrade and downgrade. The check for the version is currently very primitive, it will run a vault --version and will substring check it for the version number, so currently it is possible that a different version will be detected as the same, for example 1.7.2 will match 11.7.2 or 1.7.2.0.

The backend currently supported is raft.

Certificates need to be added manually, and if to be deployed with this, a task added to copy them.
TLS is default off as it will need the certificates to complete deployment, this is set via the following variables:

- vault_tls_disabled: true
- vault_tls_cert: test
- vault_tls_key: test
- vault_tls_version: tls12

If vault_tls_disabled is set to false, the cert and key need to be filled in and copied to the server.

vault_tls_version defines the minumum TLS version, valid values are tls10, tls11, tls12, tls13


The value UI is enabled by default, but can be turned off via vault_ui_enabled.