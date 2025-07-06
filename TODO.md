# ✅ Game Submission + Validation Schema — TODO

This document outlines the requirements to support secure and verifiable chess game submission between two players.

---

## 📦 Objectives

- Accept chess game submissions (PGN format)
- Validate game structure and result
- Verify digital signatures from both players
- Generate a content-addressed game hash
- Store validated games locally and/or on IPFS
- Optionally sync with other nodes

---

## 📝 PGN Handling

- [ ] Define PGN schema (required headers: Event, Site, Date, White, Black, Result, etc.)
- [ ] Implement PGN parser (use existing library if possible)
- [ ] Normalize PGN (consistent formatting before hashing)
- [ ] Extract metadata: player identities, result, timestamps, move list

---

## 🔐 Digital Signatures

- [ ] Define payload for signature (e.g., canonicalized PGN + metadata JSON)
- [ ] Decide signature format: EIP-712 typed data vs raw `eth_sign`
- [ ] Implement signing mechanism (e.g., SIWE or wallet-based)
- [ ] Implement verification for:
  - [ ] Player A's signature
  - [ ] Player B's signature

> Optional: support single-player submissions verified against external APIs (Lichess, Chess.com)

---

## 🧾 Game Submission Spec

Define the schema for game submissions:

```ts
interface GameSubmission {
	pgn: string; // Raw PGN text
	metadata: {
		white: string; // wallet address or DID
		black: string;
		result: "1-0" | "0-1" | "1/2-1/2";
		submittedBy: string; // sender wallet
		timestamp: number; // Unix timestamp
	};
	signatures: {
		whiteSig?: string;
		blackSig?: string;
	};
}
```

## 🔁 Validation Pipeline

- [ ] Validate PGN structure
- [ ] Validate player addresses (e.g., Ethereum checksum)
- [ ] Ensure both players signed the same payload
- [ ] Compute content hash (e.g., keccak256(canonicalGameSubmission))
- [ ] Reject duplicates or invalid submissions
- [ ] Emit game event (e.g., save to local DB, publish to pubsub, etc.)

## 📤 Persistence

- [ ] Store game record by hash locally (RocksDB/Postgres/JSON file)
- [ ] Optionally pin game file to IPFS/Filecoin
- [ ] Associate hash with both players for indexing

## 🔄 Sync Protocol Prep (Future)

- [ ] Hash-based indexing (e.g., /game/:hash)
- [ ] Support game export and import between nodes
- [ ] Add optional Merkle tree or CRDT strategy to reconcile multiple submissions

## 🧪 Tests & Edge Cases

- [ ] Malformed PGNs
- [ ] Same game submitted with different timestamps
- [ ] Signature mismatch (e.g., malicious submission)
- [ ] Player refusing to sign
- [ ] Anonymous / pseudonymous submissions

## 🧰 Dependencies

- [ ] PGN parser (e.g., chess.js, pgn-parser, or chessops)
- [ ] ethers.js or viem for signing & verification
- [ ] IPFS client (js-ipfs, @nftstorage/client, etc.)
- [ ] Hashing utility (e.g., keccak256, sha256)
