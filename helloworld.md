---
hip: xxxxx
title: Guardian Standard Registry Discovery 
author: Paul Madsen <paul@hbar.fund>
type: Standard
needs-council-approval: No
status: Active
discussions-to:
last-call-date-time: 2022-04-15T07:00:00Z
created: 2022-10-01

---

## Abstract

This HIP specifies a mechanism by which Standard Registries can register themselves such that other actors can discover them. 

## Motivation

Why do we want to enable discovery?

## Rationale

Why use HCS & a well-known topic?

## Specification

A Standard Registry registers itself for subsequent discovery by sending a Hedera Consensus Service (HCS) message to a pre-defined topic. 

Below is an example message

```
{
	'type': 'Standard Registry',
	'id': '35c5d340-1a93-475d-9659-818bb77d45df',
	'did': 'did:hedera:testnet:vzN41A2bMhvYGhg7oCMoo5UAzQ6PCTq4VTQaNPE1uPG;hedera:testnet:tid=0.0.3423402',
	'action': 'Init',
	'topicId': '0.0.34234020',
	'lang': 'en-US',
    'attributes' : {
    	'ISIC': '051 062',
    	'geography' : 'USA CAN EU AUS',
    	'law': 'USA',
    	'tags': 'VERRA iREC'
  }
}
```

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
