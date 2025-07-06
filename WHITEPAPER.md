# ♟️ The Decentralized Chess Protocol

### A peer-powered protocol for verifiable chess game history, open ratings, and community-driven reputation.

---

## 🎯 Abstract

The Decentralized Chess Protocol introduces a permissionless, tamper-proof network for recording chess games, computing player ratings, and maintaining a shared history of skill. Inspired by the architecture of Farcaster (social graph) and Filecoin (decentralized storage), the protocol allows anyone to run a node, submit games, and contribute to a transparent chess ecosystem.

---

## 🧱 Architecture Overview

### 1. Nodes (`ChessNodes`)

- Nodes are lightweight peers that validate, store, and sync chess games.
- Anyone can run a node to help scale the network and maintain game availability.

### 2. Game Submission

- Players submit signed PGNs (game records), optionally co-signed by their opponents.
- Games are verified and stored locally and optionally pinned to IPFS/Filecoin for permanence.

### 3. Identity & Trust

- Players use wallets or DIDs to sign games.
- Optional Web2 attestations (e.g., Lichess usernames) can be issued using EAS or similar systems.

### 4. Rating Engine

- Nodes compute ratings (ELO, Glicko, etc.) deterministically using open-source logic.
- Ratings are derived from verifiable game histories and can be cross-checked across nodes.
- Optional on-chain publishing of ratings enables global chess reputation.

### 5. Federation & Sync

- Nodes communicate using libp2p or gossip protocols to share new games and ratings.
- Data structures are eventually consistent (via CRDT or snapshot sync).
- Faulty or spammy peers can be blacklisted at the local level.

---

## 💡 Why Decentralize Chess?

- **Immutability**: Games cannot be deleted or falsified.
- **Interoperability**: A shared, open dataset for app builders and analysts.
- **Reputation**: On-chain ELO and player attestations form the basis of verifiable skill.
- **Permissionless Innovation**: Anyone can extend or build on the protocol (tournaments, puzzles, etc.).

---

## 🔧 Key Technologies

| Component       | Technology                            |
| --------------- | ------------------------------------- |
| Identity        | Ethereum + SIWE + EAS                 |
| Storage         | IPFS / Filecoin / RocksDB             |
| Sync            | libp2p / GossipSub / Automerge        |
| Rating Logic    | Deterministic ELO/Glicko Modules      |
| Contracts (opt) | Ethereum / Base for proofs and prizes |

---

## 🌍 Use Cases

- **Global leaderboard** with transparent rating logic
- **On-chain chess passport** aggregating games, stats, and titles
- **Tournaments with prize escrow**, managed by smart contracts
- **Proof-of-play** for NFT moments or coaching credentials
- **Cross-platform profiles** integrating Lichess, Chess.com, and wallets

---

## 🚧 Roadmap

- ⏳ Game submission + validation schema (PGN + signature)
- ⏳ Node prototype (local + IPFS storage, sync via libp2p)
- ⏳ Glicko rating module (open-source and verifiable)
- ⏳ Identity linking + EAS attestation system
- ⏳ Public explorer for games, players, and tournaments

---

## 🤝 Open Invitation

This protocol is meant to be co-owned by the chess and developer community. Whether you're a grandmaster, engineer, or enthusiast — you're invited to shape the future of decentralized chess.

> Protocol repo: `github.com/decentralized-chess/protocol`  
> Community chat: `discord.gg/dechess`  
> License: MIT

---
