# coins
A currency based on data storage and distributed data storage supported by payments.

API:
* types: 
  * digest: ```u128``` or something that can represent a digest of a dataset
  * id: Since buffers are content addressed, id is the same as a digest, but used to identify a buffer.
  * buffer: ```byte[]``` It is assumed to transmit a size first to allow receivers to exit earily if offer is too small.
  * provider: Something like a URL to represent other participants
  * offer: reference to coins held in escrow.
* calls
  * ```digest(offer: coin, identity: id, salt: digest): digest```: proof that the provider is storing the dataset.  A provider refusing to return a digest only means that the offer for the digest was too small, not that the data is gone.  This allows for negotiation of the price.  It may need another response of "I don't have the dataset". Not having the data doesn't mean that the provider will not to be able to find the data and start storing it if the offier is high enough.
  * ```get(offer: coin, identity: id): buffer```: return the dataset to the client
  * ```put(offer:coin, buffer): boolean```: push data to this provider.  If the offer is too small, the provider can exit early.
  * ```introductions(): endpoints[]```: discover the network.

1. An agent will "put" data on a provider.
2. Periodically, the agent would request a digest of a subset of that data.
  * When provided correctly, coins are transfered from the requestor to the provider.
3. requesting the data will cost more than just requesting a digest.

Providers will be encitivised to provide storage service based on ongoing payments for validation and a possible payment to return the data.

Open questions:

How can the client be assured that multiple providers aren't a fascade to a single provider that will be able to hold the data as ransom?  How can we avoid a providere "cornering the market" on a dataset?  
* Would small blocks and no client ID be enough?
* Can escrow agents hide the client?  You can't trust an anonymous escrow agent.  Escrow agents reputation would factor in, requiring a market for escrow as well.

How can network discovery work?  ```introductions()``` Seems fragile.  May lead to a network of fascdes for a bad actor.
