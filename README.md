# coins
A currency based on data storage and distributed data storage supported by payments.

API:
* types: 
  * id: ```u128``` or something that can represent a digest
  * buffer: ```byte[]``` It is assumed to transmit a size first to allow receivers to exit earily if offer is too small.
  * provider: Something like a URL to represent other participants
  * offer: reference to coins held in escrow.
* calls
  * ```digest(offer: coin, identity: id, start: usize, end: usize): u128```
  * ```get(offer: coin, identity: id): buffer```
  * ```put(offer:coin, buffer): id``` push data to this provider.  If the offer is too small, the ovider can eit early.
  * ```introductions(): endpoints[]```

1. An agent will "put" data on a provider.
2. Periodically, the agent would request a digest of a subset of that data.
  * When provided correctly, coins are transfered from the requestor to the provider.

IDs are digests.

Providers will be encitivised to provide storage service based on ongoing payments for validation.

Any data 

