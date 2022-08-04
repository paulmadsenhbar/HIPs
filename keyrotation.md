---
hip: xxxxx
title: Key Rotation
author: Paul Madsen <paul@hbar.fund>, Jo@meeco, justin@SL
type: Standard
needs-council-approval: No
status: Active
discussions-to:
last-call-date-time: 2022-04-15T07:00:00Z
created: 2022-08-01

---

## Abstract

This HIP specifies a mechanism for protecting Hedera accounts, topics, and tokens etc from key takeover. An account owner can 'pre-announce' a public key when creating the state entity such that subsequent key management operations like AccountUpdate must be signed by the private key associated with the pre-announced key to be considered valid. In this manner, even if an account's key is stolen , the attacker will be unable to take over the account as they will not have the pre-announced key.

## Motivation

There is security value in being able to keep a private key for sensitive adminstrative transactions on Hedera state entities in cold storage. This mechanism allows s private key used solely for key rotation oeprations to be annoucned to the hedera network as 'pre-rotated', ie provisioned as the *next* key in a sequence. Once pre-announced, this key can be  maintained in cold storage.

The only way the attacker can take over the private key infrastructure, is to steal the pre-rotated private key. But a number factors make this extremely difficult:

- The attacker does not even know what the pre-rotated public key is because all that has been published is its digest.
- The pre-rotated key pair does not need to be exposed in any signing operations until the next key rotation event.
- The pre-rotated key pair can be safely stored offline under very high security because it is not needed until it is placed into active service after the next key rotation event.
- Each pre-rotated key pair can be used to safely generate the next one prior to going into active service.
- Pre-rotation can even be quantum secure as long as the digest function uses a quantum-secure cryptographic hash function.


## Rationale

Hedera supports a powerful muti-signatue model by which the risk of compromise of indivodual private keys can be mitigated. However, Hedera does not allow administrative actions such as AccountUpdate to have different multi-sig requirements than the day to day transactions. Consequently, while would be possible to stipulate a multi-sig rule with multiple keys and keep one or more in cold storage, 

## Specification

The hash of a private key is provisioned via the transaction that creates the hedera state entity. 

The pre-rotation will ensure that the key controller not only announces the new public key, but also ally commitment to the next public key (called the pre-rotated public key). This commitment is in the form of a digest of the pre-rotated public key.


1. an account is created - 2 keys are provided. 1 will be the one used for , the other will be the hash of that pre-announced
2. nodes store the first key and the hash of the second
3. some time later, the account owner suspects the first key is compromised and decides to rotate
4. create an AccountUpdate tx signed by the previously pre-announced key (and also providing another hash of a 3rd key)
5. nodes verify that the tx is signed by the private key associated with the previously pre-announced key
6. nodes 

## Backwards Compatibility

## Security Implications

## How to Teach This

## Rejected Ideas

## Open Issues

N/A

## References


## Copyright/license

This document is licensed under the Apache License, Version 2.0 -- see [LICENSE](../LICENSE) or (https://www.apache.org/licenses/LICENSE-2.0)
s
