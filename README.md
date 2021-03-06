<pre>
  BIP: bip-kefkius-multicoin-multisig
  Title: Multi-Currency Hierarchy For Use In Multisignature Deterministic Wallets
  Author: Tyler Willis <kefkius@maza.club>
  Status: Draft
  Type: Standards Track
</pre>

## Abstract ##

This BIP defines a hierarchy based on BIP-0044 for deterministic wallets intended to facilitate multi-currency, multisignature wallet management.

This BIP is an application of BIP-0043.

## Motivation ##

The hierarchy defined in BIP-0044 places a coin's type level above the level designating account number. This limits the possible implementations of multi-currency, multisignature wallets. The hierarchy defined here facilitates the creation of wallets intended to be both multi-currency and multisignature.

## Specification ##

### Path Levels ###

<pre>
m / purpose' / wallet' / coin_type / change / address_index
</pre>

#### Purpose ####

Purpose is a constant tentatively set to `bip-kefkius-multicoin-multisig` as there is no BIP number assigned to this proposal. Hardened derivation is used here.

#### Wallet ####

This level is incremented for every wallet that one makes. Much like the account node in BIP-0044, this is intended to organize independent identities within the key space.
Basically, each index in this level represents a group of cosigners. Hardened derivation is used here.

#### Coin Type ####

This is the BIP-0044 index of the coin being managed. Public derivation is used here.
Public derivation is used so that cosigners need only know one of each other's public keys, rather than needing to distribute public keys for each coin.

#### Change ####

0 is used for public addresses and 1 is used for change addresses. Identical to BIP-0044 behavior. Public derivation is used here.

#### Address Index ####

The address index. This increases sequentially as it does in BIP-0044. Public derivation is used here.


## Examples ##

| wallet | coin      | change? | address | path                         |
|:-------|:----------|:--------|:--------|:-----------------------------|
| first  | Bitcoin   | no      | first   | m / bip-kefkius-multicoin-multisig' / 0' / 0  / 0 / 0   |
| first  | Bitcoin   | no      | second  | m / bip-kefkius-multicoin-multisig' / 0' / 0  / 0 / 1   |
| first  | Testnet   | no      | first   | m / bip-kefkius-multicoin-multisig' / 0' / 1  / 0 / 0   |
| second | Bitcoin   | no      | first   | m / bip-kefkius-multicoin-multisig' / 1' / 0  / 0 / 0   |
| second | Bitcoin   | yes     | first   | m / bip-kefkius-multicoin-multisig' / 1' / 0  / 1 / 0   |
| third  | Testnet   | yes     | sixth   | m / bip-kefkius-multicoin-multisig' / 2' / 1  / 1 / 5   |
