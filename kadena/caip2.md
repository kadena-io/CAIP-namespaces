---
namespace-identifier: kadena-caip2
title: Kadena Namespace - Chains
author: Ashwin van Dijk (@ash-vd)
discussions-to: https://github.com/ChainAgnostic/CAIPs/pull/60
status: Draft
type: Standard
created: 2023-06-16
requires: CAIP-2
---

# CAIP-2

_For context, see the [CAIP-2](https://github.com/ChainAgnostic/CAIPs/blob/master/CAIPs/caip-2.md) specification._

## Rationale

In CAIP-2, a general blockchain identification scheme is defined. This is the implementation of CAIP-2 for Kadena.

Kadena comprises multiple networks: a production network (mainnet), a public testing network (testnet), and a local development network (development), also known as devnet.

## Syntax

The namespace "kadena" refers Kadena's open-source blockchain platform.

## Test Cases

```
# Kadena Mainnet
kadena:mainnet

# Kadena Testnet
kadena:testnet

# Kadena Development
kadena:development
```

## References

- [CAIP-2](https://github.com/ChainAgnostic/CAIPs/blob/master/CAIPs/caip-2.md)
- [Kadena documentation](https://docs.kadena.io/)

## Copyright

Copyright and related rights waived via [CC0](https://creativecommons.org/publicdomain/zero/1.0/).
