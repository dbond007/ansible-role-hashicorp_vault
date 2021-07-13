# ansible-role-hashicorp_vault

This role will install Hashicorp Vault via download, it will configure it using raft as a backend, allow enabling tls and initialising with plain text keys or pgp.

It will download the version specified and install it, if a version is currently installed it will check if it is different to the one requested, if so, will upgrade / downgrade it.
If vault_auto_restart: true is set, it will automatically restart the vault server (requiring and unseal)

The backend currently supported is raft.

Certificates need to be added manually, and if to be deployed with this, a task added to copy them.
TLS is default off as it will need the certificates to complete deployment, this is set via the following variables:

- vault_tls_disabled: true
- vault_tls_cert: test
- vault_tls_key: test
- vault_tls_version: tls12

If vault_tls_disabled is set to false, the cert and key need to be filled in and copied to the server.
If the TLS settings are changed, the vault config will be automatically reloaded.

vault_tls_version defines the minumum TLS version, valid values are tls10, tls11, tls12, tls13

The value UI is enabled by default, but can be turned off via vault_ui_enabled.

Vault will be automatically initialised if the vault is uninitialised.
The unseal and root token will be returned in plain text in

- vault_unseal_keys
- vault_unseal_keys_b64
- vault_root_token

Unless vault_pgp_init: true is set and vault_pgp_keys and vault_pgp_root_key are populated with pgp publics keys. Then they will be returned encrypted.

Requires collection:
- ansible.posix.firewalld