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

## Abstract

CAIP-2 defines a general blockchain identification scheme.
It is a way of indentify specific networks within a blockchain ecosystem.

This is the implementation of CAIP-2 for the Kadena ecosystem.

## Specification

### Syntax
Kadena's [CAIP-2](https://github.com/ChainAgnostic/CAIPs/blob/master/CAIPs/caip-2.md) Chain ID is formatted as:

```
<namespace> + ":" + <reference>
```
- `<namespace>`: `string` - always defined as "kadena".
- `<reference>`: `string` - a unique network ID within the blockchain ecosystem (e.g. `testnet04`, `mainnet01`).

### Semantics
`Chain IDs`, as defined here, are semantically specific to the CAIP standard and are not equivalent to a Kadena "Chain ID" (e.g. chain 1).
The CAIP `Chain IDs` are more closely related to Kadena's `networkId` field.

## Rationale

Kadena comprises of multiple networks: a production network (`mainnet01`); a public testing network (`testnet04`); and a local development network (`development`), also known informally as devnet.

A CAID-2 identifier for a Kadena chain, therefore, consists of the namespace prefix (`"kadena"`) followed by the reference identifier for a network (e.g. `testnet04`). The number at the end identifies the number of times the specific network has been restarted.

### Resolution Method

To resolve a network identifier for the Kadena namespace, query the `/info` endpoint of a blockchain node.
For example,
```
// Request
$ curl https://<node-ip-or-hostname>/info
```

```jsonc
// Response
{
  "nodeNumberOfChains": 20,
  "nodeApiVersion": "0.0",
  "nodeLatestBehaviorHeight": 3774424,
  "nodeChains": ["12","13","14","15","8","9","10","11","4","5","6","7","0","16","1","17","2","18","3","19"],
  "nodeVersion": "mainnet01",
  "nodeGraphHistory": [[852054,[[12,[13,11,2]],[13,[12,14,3]],[14,[13,15,4]],[15,[14,0,16]],[8,[5,6,3]],[9,[4,6,7]],[10,[11,0,19]],[11,[12,10,1]],[4,[14,9,19]],[5,[8,7,0]],[6,[8,9,1]],[7,[9,5,2]],[0,[15,10,5]],[16,[15,1,17]],[1,[11,6,16]],[17,[16,2,18]],[2,[12,7,17]],[18,[17,3,19]],[3,[13,8,18]],[19,[10,4,18]]]],[0,[[8,[9,7,3]],[9,[8,4,5]],[4,[9,1,2]],[5,[9,6,0]],[6,[5,7,1]],[7,[8,6,2]],[0,[5,2,3]],[1,[4,6,3]],[2,[4,7,0]],[3,[8,0,1]]]]]
}
```

The response will return as a JSON value with a field labeled `nodeVersion`.
This should be used as the network identifier (i.e. "reference") in the CAIP-2 standard.

## Test Cases

```
# Kadena Mainnet
kadena:mainnet01

# Kadena Testnet
kadena:testnet04

# Kadena Development
kadena:development
```

## References

- [CAIP-2](https://github.com/ChainAgnostic/CAIPs/blob/master/CAIPs/caip-2.md)
- [Kadena documentation](https://docs.kadena.io/)

## Copyright

Copyright and related rights waived via [CC0](https://creativecommons.org/publicdomain/zero/1.0/).
