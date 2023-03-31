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

This HIP specifies a binding of the DIF Presentation Exchange pattern to IPFS & Hedera Consensus Service as part of the Guardian architecture. An authorized actor (e.g.an Auditor or Regulator) is able to access non-public attributes associated with a sustainability project by proof of their certications attached to an HCS message requesting that access. By using HCS, we ensure a provable history of request & response for such protected attributes.

## Motivation

The Guardian Selective Disclosure architecture allows a Guardian admin to stipulate what attributes within a Verifiable Credential (VC) should not be available to the 
public, but rather only to authorized requestors. For such a VC, the corresponding Verifiable Presentation (VP) published to IPFS will not contain those protected attributes, but rather a 'Presentation Definition' indicating the nature of the proof required to access them. If and when some other actor is able to demonstrate the stipulated proof on a request as a 'Presentation Submission', the protected attributes will be released to them. 

## Rationale

The DIF Presentation Exchange specification (https://identity.foundation/presentation-exchange/) defines an abstract pattern between a Verifier and a Holder - specifically 
"a way for Verifiers to describe proof requirements, and for Holders to describe submissions of proof which align with those requirements."

This specification defines a binding of this abstract pettern for the Guardian Selective Disclosure architecture that uses IPFS & Hedera Consensus Service (HCS)

## Specification

### High-Level Flow

1. A Guardian implementation publishes a protected VP to IPFS. The VP indicates that there are non-public attributes available to requestors that have a certain role. 
2. An Auditor is notified of the availability of the non-public attributes. 
3. The Auditor, acting as a Verifier, creates an HCS message requesting access to the non-public VP. The HCS message carries a separate VP proving their certification. The HCS message is submitted to the Hedera network. This is the Presentation Request.
4. The Presentation Exchange Responsder, acting as a Holder, is notified of the request. It validates the Verifiers's authorization VP and compares the certifications within the Verifier's VC to the authorization policy for the protected VP.

### Presentation Definition



### Presentation Submission



## Backwards Compatibility
 
## Security Implications

## How to Teach This

## Rejected Ideas

## Open Issues

## References

## Copyright/license

This document is licensed under the Apache License, Version 2.0 -- see [LICENSE](../LICENSE) or (https://www.apache.org/licenses/LICENSE-2.0)
