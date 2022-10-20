---
hip: xxxxx
title: Guardian Standard Registry Discovery 
author:lots of contributors eventually 
type: Standard
needs-council-approval: No
status: Active
discussions-to:
last-call-date-time: 
created: 2022-10-01

---

## Abstract

This HIP specifies a mechanism by which Guardian-enabled Standard Registries (SR) can announce themselves such that other actors can discover them, along with the artefacts and tokenized assets representing ESG credeits & debits. 

At the time of inititialization, a SR sends an initialization (a.k.a. 'Hello World') message to a shared Hedera Consensus Service (HCS) topic broadcasting its existence, attributes, and the specific HCS topic which would become dedicated 'root' for its ontology of topics into which it will send its own subsequent messages. 

The history of these 'Hello World' messages sent to this shared topic by different SRs consequently acts as a catalog of all Guardian-enabled SRs. Other participants in the ecosystem can query this history to discover SRs that might be of interest - particularly to discover the tokenized assets minted by that SR.

This HIP normalizes the 'Hello World' mechanism.

## Motivation

Why do we want to enable discovery?

## Rationale

HCS provides a trusted & provable log of events. Messages are submitted to the Hedera network for consensus, given a trusted timestamp, and fairly ordered. 

The messages submitted to a particular topic over time are stored by Hedera mirror nodes. The history of messages for any topic can be queried by any application.

Applications can subsribe to an HCS topic so that they are informed of new messages for that topic.

 HCS allows any SR to announce its existence to the community and for interested applications to both be informed of those new SRs and, if of interet, to navigate to the corresponding tokens and their trust chains. 

### Shared Discovery Topic Identifier

The official shared discovery topic identifier is 0.0.xxxxxx

### Message Schema

A Standard Registry registers itself for subsequent discovery by sending a Hedera Consensus Service (HCS) message to a pre-defined topic.

The message if formatted as a JSON object, with an extendable set of attributes. The following attributes are mandatory:
- 'type': should have 'Standard Registry' value.
- 'id': UUID of the message.
- 'did': DID of the Standard Registry sending the message.
- 'action': should have 'Init' value.
- 'topicId': the ID of the root topic for this Standard Registry.
- 'lang': contains the language/encoding of the messages produced by this Standard Registry.

The 'attributes' section is optional, Standard Registries can chose which specific properties/attributes of their functionality need to be announced to the world. We anticipate the emergence of best practices for different industry sectors and geographic areas, this format was created to accomodate such potential future developments.

Below is an example message

```
{
	'type': 'Standard Registry',
	'id': '35c5d340-1a93-475d-9659-818bb77d45df',
	'status':'ISSUE',
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
The above message announces a new SR and its associated HCS topic identifier. The attributes allow actors who read this messages from the shared topic history to determine if the SR and its associated tokenized assets are of interest. If so, they can query the SR specific topic identifier (0.0.34234020 in above) to dig deeper and find those associated assets and their full provenance chain.

### Topic Mutability

If an HCS topic has an admin key, then it can be updated/modified.

The Guardian shared discovery topic has no admin key and as such, cannot be modified once created and so can be considered immutable.

### Topic Submission Authorization

Authorization for submission against an HCS topic is controlled by the topic owner stipulating a list of public keys. Only messages signed by the corresponding private key will be authorized.

The Guardian shared discovery topic has no submission keys and as such, any actor can submit to the shared topic. Consequently, the existence of an entry for a SR in the history for the shared topic should not be interpreted as endorsement or certification.

## Backwards Compatibility

n/a

## Security Implications

## How to Teach This

## Rejected Ideas

## Open Issues

N/A

## References

## Copyright/license

This document is licensed under the Apache License, Version 2.0 -- see [LICENSE](../LICENSE) or (https://www.apache.org/licenses/LICENSE-2.0)
s
