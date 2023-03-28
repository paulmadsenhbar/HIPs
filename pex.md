---
hip: xxxxx
title: Guardian Binding for Presentation Exchange
author: 
type: Standard
needs-council-approval: No
status: Active
discussions-to:
last-call-date-time: 
created: 2023-02-10

---

## Abstract

This HIP specifies a binding of the DID Presentation Exchange pattern to IPFS & Hedera Consensus Service as part of the Guardian architecture.

## Motivation

the Guardian Selective Disclosure architecture allows a Guardian admin to stipulate what attributes within a Verifiable Credential (VC) should not be available to the 
public, but rather only to authorized requestors. For such a VC, the corresponding Verifiable Presentation (VP) published to IPFS will not contain those protected attributes, 
but rather an 

This logical interaction 

## Rationale

The DID Presentation Exchange specification (https://identity.foundation/presentation-exchange/) defines an abstract pattern between a Verifier and a Holder - specifically 
"a way for Verifiers to describe proof requirements, and for Holders to describe submissions of proof which align with those requirements."

This specification defines a binding of this abstract pettern for the Guardian Selective Disclosure architecture that uses IPFS & Hedera Consensus Service (HCS)

## Specification

### Presentation Definition

How does a Verifier create and publish to Holders a Definition?

### Presentation Submission

How does a Holder present a VP that meets the requirements of the Definition? 

## Backwards Compatibility
 
## Security Implications

## How to Teach This

## Rejected Ideas

## Open Issues

## References

## Copyright/license

This document is licensed under the Apache License, Version 2.0 -- see [LICENSE](../LICENSE) or (https://www.apache.org/licenses/LICENSE-2.0)
