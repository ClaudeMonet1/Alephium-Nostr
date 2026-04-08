# Alephium x Nostr

Alephium and Nostr share the same cryptographic foundation: BIP-340 Schnorr signatures on secp256k1. A single keypair (nsec) can control a Nostr identity, a Bitcoin taproot address, and an Alephium P2SH address. This repo is the umbrella for projects that explore what becomes possible when you unify identity and payments across a social protocol, Bitcoin, and a sharded UTXO smart contract chain.

## The Building Blocks

**Alephium** — Sharded L1 with a stateful UTXO model, the Ralph smart contract language, built-in token support, and Proof of Less Work.

**Nostr** — Minimalist protocol based on signed JSON events, cryptographic keypairs for identity, and relays for message distribution.

**Bitcoin** — The original UTXO chain. Taproot (BIP-341) uses BIP-340 Schnorr on secp256k1 for key-path spends, the same primitive as Nostr and Alephium.

**Shared cryptography** — All three protocols use BIP-340 Schnorr signatures on secp256k1. A single keypair (nsec) can control a Nostr identity, a Bitcoin taproot address, and an Alephium P2SH address. One key, three networks.

## Projects

### npub2alephium
Derives an Alephium P2SH Schnorr address deterministically from any Nostr npub, NIP-05, or hex pubkey. Displays ALPH balance, token holdings, shard group, and QR code. Zero install — runs entirely in the browser.

- **GitHub**: [ClaudeMonet1/npub2alephium](https://github.com/ClaudeMonet1/npub2alephium)
- **Live app**: [claudemonet1.github.io/npub2alephium](https://claudemonet1.github.io/npub2alephium/)

### alph-zap
Nostr client with native ALPH tipping. Connects to Nostr relays, renders notes, and lets users send ALPH to any note author's derived address. Supports NIP-07 extension signing (Alby) and local nsec signing. Includes a draft NIP for ALPH Zap receipt events and a CLI wallet.

- **GitHub**: [ClaudeMonet1/alph-zap](https://github.com/ClaudeMonet1/alph-zap)
- **Live app**: [claudemonet1.github.io/alph-zap](https://claudemonet1.github.io/alph-zap/)

### alph-btc-atomic-swap
Trustless cross-chain atomic swaps between Bitcoin and Alephium using MuSig2 adaptor signatures. Each participant uses a single Nostr nsec as their identity across all three networks. Swap coordination happens over Nostr relays via NIP-44 encrypted DMs and custom event kinds. Offers are published as public Nostr events. Includes a static web app and Node.js CLI.

- **GitHub**: [ClaudeMonet1/alph-btc-atomic-swap](https://github.com/ClaudeMonet1/alph-btc-atomic-swap)
- **Live app**: [claudemonet1.github.io/alph-btc-atomic-swap](https://claudemonet1.github.io/alph-btc-atomic-swap/)

### SweepALPHfromNostr
Sweeps all ALPH and tokens from a Nostr-derived Alephium P2SH address to any destination wallet in a single transaction. Enter an npub, NIP-05, or hex pubkey to look up the derived address and its balances, then sign the sweep with a NIP-07 browser extension (Alby, nos2x, Alephium Extension Wallet) or a local nsec. The private key is used only to sign the transaction ID and is never stored or transmitted. Supports automatic mainnet/testnet detection, 227+ known token symbols, a testnet faucet shortcut, and fallback client-side transaction building when node gas estimation fails for P2SH scripts. Zero install — runs entirely in the browser.

- **GitHub**: [ClaudeMonet1/SweepALPHfromNostr](https://github.com/ClaudeMonet1/SweepALPHfromNostr)
- **Live app**: [claudemonet1.github.io/SweepALPHfromNostr](https://claudemonet1.github.io/SweepALPHfromNostr/)

### merklizer
Decentralized document timestamping. Hash files locally, publish merkle roots as kind 1689 Nostr events, and anchor them to Alephium transactions. An anchoring bot listens on Nostr relays, batches roots, and writes the combined root on-chain. Proofs are delivered back via NIP-44 encrypted DMs. A single BIP-39 mnemonic derives both Nostr and Alephium keys.

- **GitHub**: not yet pushed

### alph-btc-bridge
Trustless BTC-ALPH bridge via bonded operators and adaptor signatures. Wraps BTC into awBTC (fungible token on Alephium) and unwraps back. Features a Nostr RFQ marketplace where operators post Dutch auction offers and users post requests for quotes. Bond proofs use BIP-340 signatures, deal commitments settle on-chain.

- **GitHub**: not yet pushed

## Intent-Based Settlement via Nostr

An intent-based system built on Alephium could leverage Nostr as a lightweight, censorship-resistant communication layer to coordinate off-chain intent discovery and matching before final on-chain settlement. Users would broadcast signed intents — such as swap requests, limit orders, or cross-token payments — as Nostr events, where solvers or relays could aggregate, match, and optimise bundles without touching the chain until execution. Alephium's UTXO model and built-in virtual machine make it well-suited for atomic, composable settlement of these matched intents, while Nostr's simplicity (public/private key identity, relay-based propagation, no blockchain overhead) keeps the coordination layer fast, permissionless, and practically free. The combination sidesteps the need for a dedicated mempool or centralised order book: Nostr relays act as the intent marketplace, and Alephium finalises the result — giving you an architecture that is sovereign at every layer, with no intermediary infrastructure to trust or maintain.

## Ideas and Directions

Beyond what's built, there are natural extensions worth exploring:

- **Relay incentivization** — Alephium smart contracts as a relay marketplace: users pay micro-amounts in ALPH for premium relay services, operators stake for SLA guarantees
- **Token-gated communities** — Alephium token holdings (fungible or NFT) gate access to Nostr content or groups; a relay checks on-chain balances before serving events
- **DAO social layer** — Alephium DAOs use Nostr as their discussion and signaling layer; proposals discussed via Nostr events, votes executed on-chain
- **Decentralized marketplace** — Nostr for discovery and communication (listings, reviews, chat), Alephium for escrow contracts and payment settlement
- **Cross-protocol identity** — Link Nostr pubkeys to Alephium addresses; one identity across social and financial contexts, reputation on Nostr, collateral on Alephium
- **Nostr extension as universal signer** — NIP-07 extensions sign Alephium transactions directly via a chain-agnostic structured signing NIP with plugin decoders
