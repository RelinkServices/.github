# Relink Protocol - Trustless Chainlink Relaying Service

The Relink Protocol provides a trustless way to integrate the bluechip oracle provider Chainlink into any smart contract platform.

### Philosophy

In recent years, several projects have proven excellent basic services and have been widely accepted by dapp developers. However, in the same time the amount of available networks has grown very much, so that these providers can serve only a part of the existing networks.

We believe that superb services should be available on as many chains as possible. And we also believe in the decentralized approach and that the community should be empowered to integrate beloved services permissionless into their own networks.

Every Dapp developer should have access to blue-chip data providers and not have to compromise with second-rate services just because their preferred services are not available.

### How Relink Achieve This Vision

Relink provides a relaying service by providing base contracts that has implemented a similar interface as the original base consumer contract. The relaying service forwards the request to an officially supported chain and as soon as the results arrive, the result is played back to the target network along with signatures from the Relink Oracle network.

These signatures are checked by the dapp contract so that malicious behavior of the relaying service would be detected and the callback call would fail.

In this way, Relink Services can offer Chainlink services to any smart contract platform - there is no restriction to EVM chains.

### Components & Flow

![Alt text](https://github.com/RelinkServices/.github/blob/main/Relink%20Architecture.png?raw=true)

1. The dapp calls the requestXxx method provided by the RelinkXyzConsumerBase contract. An internal call to the RelinkXyzProxy contract is initiated.

2. The RelinkXyzProxy emits an event that is recognized and processed by the Relaying Service backend.

3. The Relaying Service backend invokes the RelinkXyzProducer contract on Polygon.

4. The RelinkXyzProducer implements the ChainlinkXyzConsumerBase contract and can initiate a data request from Chainlink.

5. Chainlink calls the callback method provided by RelinkXyzProducer and passes the requested data.

6. RelinkXyzProducer emits an event that is recognized and processed by the Relaying Service backend.

7. The Relaying Service backend calls oracle nodes to extract the data from the emitted event and create a signature for the data.

8. The Relaying Service backend calls the callback method provided by the RelinkXyzProxy and passes the requested data along with the signatures.

9. The RelinkXyzProxy forwards the call to the dapp that initiated the data request.

## Relink Features

### Reuse of the Chainlink interfaces

At Relink, we take care to implement the official Chainlink interfaces as accurately as possible, so that existing code bases can be transferred almost effortlessly. This makes adapting successful dapps into other networks much more lucrative and faster.

### Pay in native token

With Relink you use the native token on the respective network. Relink takes care of exchanging the native tokens on the target network into LINK from time to time to pay for the Chainlink services.

### Non-EVM chains

Chainlink services are mainly offered on EVM compatible chains. With Relink, we enable non-EVM chains to take advantage of the world-class services of the Chainlink Oracle Network.
