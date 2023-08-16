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

## Rationale

A Kadena account can consist of one or more public keys. When creating an account with one public key the account will by default consist of `k:` proceeded by the public key. These public keys can also be rotated later, so it's important to note that the associated public key might not remain the same throughout the account's existence. When there are multiple keys associated with an account (multisig) the account will be prefixed with `w:`.

In Pact, Kadena's Smart Contract language, you can create so called guards. These guards are a way to restrict access to specific parts of a contract. A capability guard is denoted by `c:`, while a user guard is indicated by `u:`.

It's possible to create vanity accounts, where you can choose the name of your account by yourself. However, these accounts can be "squatted" on other chains: if you create an account with the name `capybara` on chain 0, someone else can create the same account on one of the other chains. For this reason this is not recommended.

A valid Kadena account has a minimum length of 3 characters and a maximum length of 256, including the prefix. An account can only contain characters in the LATIN1 charset and it cannot start with a letter followed by a colon, as this is reserved for principles.

## Syntax

The syntax of a Kadena address matches the following regular expression:

`[\x20-\x7F]{3,256}`

## Chain IDs

_For context, see the [CAIP-2](https://github.com/ChainAgnostic/CAIPs/blob/master/CAIPs/caip-2.md) specification._

| Network Name | Chain ID    |
| ------------ | ----------- |
| Mainnet      | mainnet01   |
| Testnet      | testnet04   |
| Development  | development |

## Test Cases

```
# Kadena Mainnet
kadena:mainnet01:

# Kadena Testnet
kadena:testnet04

# Kadena Development
kadena:development
```

## References

[Introducing Kadena Account Protocols (KIP-0012)](https://medium.com/kadena-io/introducing-kadena-account-protocols-kip-0012-303462b77af1)
[What are principles in Pact?](https://gist.github.com/EnoF/fdf5b4e783f8e55a4ece078b1d215fc9)
[Pact documentation](https://pact-language.readthedocs.io/en/stable/)
[CAIP-2]: https://github.com/ChainAgnostic/CAIPs/blob/master/CAIPs/caip-2.md
[CAIP-10]: https://github.com/ChainAgnostic/CAIPs/blob/master/CAIPs/caip-10.md

## Rights

Copyright and related rights waived via [CC0](https://creativecommons.org/publicdomain/zero/1.0/).
