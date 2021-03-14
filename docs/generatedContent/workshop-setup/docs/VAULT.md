# Vault

## Vault CLI

See Vault Project [Install Vault](https://www.vaultproject.io/docs/install), or Hashicorp [Install Vault](https://learn.hashicorp.com/tutorials/vault/getting-started-install).

### OSX

Homebrew formula for [Vault](https://formulae.brew.sh/formula/vault).

```bash
brew install vault
```

```bash
$ vault version
Vault v1.6.3 ('b540be4b7ec48d0dd7512c8d8df9399d6bf84d76+CHANGES')
```

### Linux

```bash
wget https://releases.hashicorp.com/vault/1.6.3/vault_1.6.3_linux_amd64.zip -P  ./vault-1.6.3
cd vault-1.6.3
unzip vault_1.6.3_linux_amd64.zip
cd ..
chmod +x vault-1.6.3/vault
echo "export PATH=$(pwd)/vault-1.6.3/:$PATH" > $HOME/.bash_profile
source $HOME/.bash_profile
vault version
```
