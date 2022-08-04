---
hip: xxxxx
title: Pre-Rotated Keys 
author: Paul Madsen <paul@hbar.fund>, Jo@meeco
type: Standard
needs-council-approval: No
status: Active
discussions-to:
last-call-date-time: 2022-04-15T07:00:00Z
created: 2022-08-01

---

## Abstract

This HIP specifies a mechanism for protecting Hedera state entities like accounts, topics, and tokens etc from takeover after key compromise. An account owner can 'pre-rotate' a public key when creating the state entity such that subsequent key management operations via AccountUpdate must be signed by the private key associated with the pre-rotated key to be considered valid. 

In this manner, even if an account's hot key is stolen , the attacker will be unable to take over the state entity as they will not have the pre-rotated key and so cannot lock the valid owner out. 

In this model, for any Hedera state entity, there can be a 'hot' key that can sign transactions, but not change the key on the state entity. There is a seprate pre-rotated key 'cold' key that is uniquely authorized to rotate the current hot key and replace it with itself. 

For enhanced security, the pre-announced cold key could self be a multi-sig with appropriate threshold rules (presumably not if we pre-announce only the digest?)

## Motivation

There is security value in being able to keep a private key for sensitive adminstrative transactions on Hedera state entities in cold storage. This mechanism allows s private key used solely for key rotation oeprations to be announced to the Hedera network as 'pre-rotated', ie provisioned as the *next* key in a sequence. Once pre-rotated, this key can be  maintained in cold storage and brought only for key rotation transactions.

The only way the attacker can take over the private key infrastructure, is to steal the pre-rotated private key. But a number factors make this extremely difficult:

- The attacker does not even know what the pre-rotated public key is because all that has been published is its digest.
- The pre-rotated key pair does not need to be exposed in any signing operations until the next key rotation event.
- The pre-rotated key pair can be safely stored offline under very high security because it is not needed until it is placed into active service after the next key rotation event.
- Each pre-rotated key pair can be used to safely generate the next one prior to going into active service.
- Pre-rotation can even be quantum secure as long as the digest function uses a quantum-secure cryptographic hash function.


## Rationale

Hedera supports a powerful muti-signatue model by which the risk of compromise of individual private keys can be mitigated. However, Hedera does not allow administrative actions such as AccountUpdate to have different multi-sig requirements than other less sensitive transactions. Consequently, while would be possible to stipulate a multi-sig rule with multiple keys and keep one or more in cold storage, it woudl be .......

## Specification

The hash of a public key is provisioned via the transaction that creates the hedera state entity. 

The pre-rotation will ensure that the key controller not only provisions a public key when creating a Hedera state entity, but can also optionally make a commitment to the next public key (called the pre-rotated public key). This commitment is in the form of a digest of the pre-rotated public key.


1. an account is created - 2 keys are provided. 1 will be the one used until rotated , the other will be the hash of a pre-rotated key
2. nodes store the first key and the hash of the second
3. Transactions are verified against the current hot key
4. some time later, the account owner suspects the hot key is compromised and decides to rotate
5. the account owner creates an AccountUpdate tx signed by the previously pre-announced key (and also optionally? providing the hash of the next pre-rotated key)
6. nodes verify that the transaction is signed by the private key associated with the previously pre-rotated key
7. nodes henceforth a) use the first pre-rotated key as the hot key and b) store the hash of the second pre-rotated key against future key rotation transactions

## Backwards Compatibility

It is optional to pre-rotate a key when creating a state entity. Any existing state entity, or any entity created with no pre-rotated key, would continue to have the existing model for key rotation.


## Security Implications

A pre-rotated key must be defined at the time of state entity creation. 

If the attacker steals the hot key, they would be able to sign all transactions other than an AccountUpdate changing the keys. As such, they would be able to send HBARs etc. It would be the actual owner's resonsibility to monitor for such fraudulent transactions and (quickly) use the pre-rotated key from cold storage to change the key and prevent the attacker from cuasing any further harm.

## How to Teach This

Provides a useful option for enhanced security of hedera state entities with different characteristics than multi-sig.

## Rejected Ideas

It could be possible to allow more rigorous multi-signature rules for AccountUpdate transactions to be defined than for other transactions. Some of those sensitive operation keys could be stored cold. However, this would still presume that they keys would be public and so possibly provide to the attacker information??

## Open Issues

N/A

## References


## Copyright/license

This document is licensed under the Apache License, Version 2.0 -- see [LICENSE](../LICENSE) or (https://www.apache.org/licenses/LICENSE-2.0)
s
