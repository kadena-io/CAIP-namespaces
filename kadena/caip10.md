---
namespace-identifier: kadena-caip10
title: Kadena Namespace - Addresses
author: Ashwin van Dijk (@ash-vd)
discussions-to: https://github.com/ChainAgnostic/namespaces/pull/26
status: Draft
type: Standard
created: 2022-08-16
requires: ["CAIP-2", "CAIP-10"]
---

# CAIP-10

_For context, see the [CAIP-10](https://github.com/ChainAgnostic/CAIPs/blob/master/CAIPs/caip-10.md) specification._

## Abstract

CAIP-10 defines a way to identify an account in any blockchain specified by CAIP-2 blockchain id.
This is the implementation of CAIP-10 for the Kadena ecosystem.

## Specification

### Syntax

Kadena's [CAIP-10](https://github.com/ChainAgnostic/CAIPs/blob/master/CAIPs/caip-10.md) Account ID is formatted as:

```
<chain_id> + ":" + <account_address>
```
- `<chain_id>`: `string` - the Kadena CAIP-2 [Chain ID](https://github.com/ChainAgnostic/namespaces/blob/main/kadena/caip2.md).
- `<account_address>`: `string` - the public key available for signing by the wallet.

### Semantics

The `chain_id` follows the [CAIP-2 standard](https://github.com/ChainAgnostic/CAIPs/blob/master/CAIPs/caip-2.md) and can be one of the following:

| Network Name | Chain ID    |
| ------------ | ----------- |
| Mainnet      | mainnet01   |
| Testnet      | testnet04   |
| Development  | development |

The `account_address` is a public key (e.g. ED22519) matching the regular expression `TODO`.

`Account IDs`, as defined here, are semantically specific to the CAIP standard.
This does not represent an account in a Kadena fungible contract (e.g. `coin`).
The motivation for this distiction can be found in [Accounts vs. Public Keys](https://github.com/kadena-io/KIPs/blob/master/kip-0017.md#accounts-vs-public-keys) in KIP-0017.

## Rationale

A Kadena account can consist of one or more public keys. When creating an account with one public key the account will by default consist of `k:` proceeded by the public key. These public keys can also be rotated later, so it's important to note that the associated public key might not remain the same throughout the account's existence. When there are multiple keys associated with an account (multisig) the account will be formatted as `w:<hash-of-public-key-list>:<predicate>`.

In Pact, Kadena's Smart Contract language, you can create so called guards. These guards are a way to restrict access to specific parts of a contract. A capability guard is denoted by `c:`, while a user guard is indicated by `u:`. These prefixed accounts are called [principal accounts](https://gist.github.com/EnoF/fdf5b4e783f8e55a4ece078b1d215fc9).

It's also possible to create vanity accounts, where you can choose the name of your account by yourself. However, these accounts can be "squatted" on other chains: if you create an account with the name `capybara` on chain 0, someone else can create the same account on one of the other chains. For this reason this is not recommended.

A valid Kadena account has a minimum length of 3 characters and a maximum length of 256, including the prefix. An account can only contain characters in the LATIN1 charset and it cannot start with a letter followed by a colon, as this is reserved for principles.

Given the wide range of formats that a Kadena Account can have, it is **highly discouraged** to assume that the public keys returned in
CAIP-10 Account IDs are `k:` accounts. This assumptions limits which types of accounts end-users can use.

Instead, Kadena has specified a standard for a [getAccounts](https://github.com/kadena-io/KIPs/blob/master/kip-0017.md#kadena_getAccounts_v1) 
method that will retrieve the Kadena accounts associated with the public key of a CAIP-10 Account ID.

## Test Cases

This is a list of manually composed examples.

```
# Kadena Mainnet
kadena:mainnet01:38298612cc2d5e841a232bd08413aa5304f9ef3251575ee182345abc3807dd89

# Kadena Testnet
kadena:testnet04:22ddc64851718e9d41d98b0f33d5e328ae5bbbbd97aed9885adac0f2d070ff9c

# Kadena Development
kadena:development:38298612cc2d5e841a232bd08413aa5304f9ef3251575ee182345abc3807dd89
```

## References

[Kadena's WalletConnect Specification (KIP-0017)](https://github.com/kadena-io/KIPs/blob/master/kip-0017.md)
[Introducing Kadena Account Protocols (KIP-0012)](https://medium.com/kadena-io/introducing-kadena-account-protocols-kip-0012-303462b77af1)
[What are Principal in Pact?](https://gist.github.com/EnoF/fdf5b4e783f8e55a4ece078b1d215fc9)
[Pact Documentation](https://pact-language.readthedocs.io/en/stable/)
[CAIP-2]: https://github.com/ChainAgnostic/CAIPs/blob/master/CAIPs/caip-2.md
[CAIP-10]: https://github.com/ChainAgnostic/CAIPs/blob/master/CAIPs/caip-10.md

## Rights

Copyright and related rights waived via [CC0](https://creativecommons.org/publicdomain/zero/1.0/).
