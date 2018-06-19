# v2bip

*v2bip* is a utility for converting Hashicorp Vault unsealing keys to easy to remember and record Bitcoin-style [BIP-39](https://github.com/bitcoin/bips/blob/master/bip-0039/bip-0039-wordlists.md) seed phrases.

This allows for users to more easily store and enter their unsealing keys versus having to rely on hard to remember base64 encoded strings that are generated by vault.

## Usage

When a new Vault instance is deployed, Unsealing Keys are generated via a Shamir scheme and displayed as base64 encoded values. These are to be store separate and securely but must be accessable if the Vault is to be unsealed. v2bip allows for converting those keys to seed phrases to that can be stored and include minor error correcting by default.

When Vault generates unsealing keys:
    Unseal Key: Bq/D1o6y619yF5NjXEwn5khTUsIVs0LZq3+ucdtRYUI=

These keys can be passed to v2bip on an airgapped machine and a phrase generated:
    $ echo -n "Bq/D1o6y619yF5NjXEwn5khTUsIVs0LZq3+ucdtRYUI=" | v2bip -e
    choose easily unit train young hello bitter rebuild dress enrich claim goose exist basic brain nature drill lava interest twenty public valley cube abandon

This phrase can be then passed back to v2bip to regenerate the unsealing key:
    $ echo "choose easily unit train young hello bitter rebuild dress enrich claim goose exist basic brain nature drill lava interest twenty public valley cube abandon" | v2bip -d
    Bq/D1o6y619yF5NjXEwn5khTUsIVs0LZq3+ucdtRYUI=