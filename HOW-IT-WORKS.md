# 🏁 Decentralized Chess Protocol

A decentralized protocol for recording chess games, computing verifiable ratings, and enabling anyone to run a node — inspired by Farcaster, Filecoin, and the spirit of open competition.

---

## 🎯 Goals

- Verifiable, tamper-proof storage of chess games
- Decentralized ELO/Glicko-based rating system
- Open node infrastructure — anyone can run a node
- Permanent, content-addressable game history
- Extensible ecosystem for tournaments, NFTs, and more

---

## 🧩 System Architecture

### 1. Nodes (`ChessNodes`)

Each node can:

- Accept & validate signed game submissions
- Store and index games locally + optionally to Filecoin/IPFS
- Serve REST/gRPC endpoints (e.g. `/player/:id/games`)
- Sync with other nodes (gossip or CRDT-based)
- Optionally compute and expose player ratings

> Inspired by [Farcaster Hubs](https://docs.farcaster.xyz/), but chess-focused.

---

### 2. Game Submission Flow

1. **Player A** submits a signed PGN to a node
2. **Player B** co-signs the result (or proof fetched from external source like Lichess API)
3. Once verified:
   - Stored locally
   - Optionally pinned to IPFS/Filecoin
   - Broadcasted to the network

---

### 3. Identity Layer

- Players identified via **wallet address** or **Decentralized ID (DID)**
- Use **Sign-In With Ethereum (SIWE)** or similar
- Optional: link to Web2 accounts via **EAS attestations** or Sismo/Zupass

---

### 4. Rating Engine

- Deterministic rating computation (e.g., **ELO**, **Glicko**, **TrueSkill**)
- Each node may run a local rating plugin
- Optionally, ratings can be:
  - Stored locally
  - Pushed to-chain for verification
- Ratings versioned & reproducible given shared game history

---

### 5. Storage Layer

- PGNs + metadata stored in:
  - IPFS/Filecoin (content-addressed)
  - Local database (PostgreSQL, RocksDB, or SQLite)
- Nodes serve:
  - `/game/:hash`
  - `/games`
  - `/player/:id`

---

### 6. Sync & Federation

- Nodes replicate data using:
  - Gossip protocol (libp2p, GossipSub)
  - CRDT-based syncing (Automerge/Yjs)
  - Periodic snapshots
- Optionally:
  - Node trust scores
  - Blacklisting of malicious/spammy peers

---

## 🛠️ Tech Stack

| Layer           | Technology                                |
| --------------- | ----------------------------------------- |
| Node Runtime    | Node.js (Hono / Fastify)                  |
| Sync Protocol   | libp2p, GossipSub, CRDT (Automerge/Yjs)   |
| Storage         | IPFS + Filecoin + RocksDB/Postgres        |
| Rating Engine   | Glicko / ELO / TrueSkill (modular plugin) |
| Identity        | SIWE, EAS, Sismo                          |
| P2P Messaging   | libp2p + GossipSub                        |
| Smart Contracts | Ethereum / Base (optional)                |

---

## 💡 Use Cases

- Tamper-proof public chess game archive
- Decentralized leaderboard with provable reputation
- Player identity + ranking as on-chain credentials
- Open tournaments with smart contract prize pools
- Chess achievement NFTs & commemorative moments

---

## 🔥 Extensions (Future)

- Lichess/FICS/FIDE game ingestion
- Frame integrations for Farcaster
- Staking-based anti-cheat incentives
- Chess puzzle leaderboard as a side module
- zk-proof of skill (zkELO?)

---

## 📦 Next Steps

- [ ] Node bootstrap repo with game submission & storage
- [ ] Signature schema for PGN verification
- [ ] CRDT-based game sync prototype
- [ ] Rating engine module (ELO/Glicko)
- [ ] Light client / explorer frontend

---

Built for and by chess nerds 🧠♟️
