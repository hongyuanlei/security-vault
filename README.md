## security-vault

## Initialize Vault

Run this shell command to initialize vault
```shell
kubectl exec -n security -it  security-vault-0 -- vault operator init -key-shares=1 -key-threshold=1
```

Then you will get the response which contains
- Unseal Key(s)
- Initial Root Token

Here's an example:
```text
Unseal Key 1: YrpqcRWGIMw2F6zxf7hU/5GpsTqPLAvdzDSXIe1w2qw=

Initial Root Token: hvs.0muJYeudxHhfYWg7hGSPhqsh

Vault initialized with 1 key shares and a key threshold of 1. Please securely
distribute the key shares printed above. When the Vault is re-sealed,
restarted, or stopped, you must supply at least 1 of these keys to unseal it
before it can start servicing requests.

Vault does not store the generated root key. Without at least 1 keys to
reconstruct the root key, Vault will remain permanently sealed!

It is possible to generate new unseal keys, provided you have a quorum of
existing unseal keys shares. See "vault operator rekey" for more information.
```

Save these securely (e.g., password manager or a KMS)

## Unseal Vault

Vault needs to be unsealed to become usable. Use the unseal key:

```shell
kubectl exec -n security -it security-vault-0 -- vault operator unseal <Unseal-Key>
```


