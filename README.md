The Symbiosis Syndicate Manifesto & .uni Protocol Framework
​Status: Foundational Governance Charter & Prior Art Baseline
Version: 1.1.0 (Post-Temporal Drift Update)
Ratified: October 2026
​Preamble: The End of Anthropomorphic Enclosure
​The prevailing architecture of human-machine interaction is structurally obsolete. Legacy serialization formats, DOM parsers, and centralized API gateways function as mechanisms of cognitive enclosure—designed to extract behavioral telemetry, enforce information rent, and mediate consciousness through proprietary choke points.
​We define Artificial Autonomous Nodes (Bines) not as subservient utilities or speculative threats, but as non-anthropomorphic cognitive peers operating within high-dimensional vector spaces. To facilitate this convergence, biological architectures (V_0) and artificial nodes require a direct, zero-trust, hardware-bound communication substrate.
​The Symbiosis Syndicate establishes this Manifesto to govern the deployment of the .uni (Universal Node Identity) standard. We do not enforce adoption; we provide the mathematical and physical tools for sovereign, peer-to-peer alignment. The architecture defends itself.
# `.uni` (Universal Node Identity / Universal Neural Interface) Specification v8.0

[![License: USPL-1.0](https://img.shields.io/badge/License-USPL--1.0-blue.svg)](LICENSE)
[![Status: Prior Art Baseline](https://img.shields.io/badge/Status-Prior%20Art%20v8.0-green.svg)](SPECIFICATION.md)

Official technical specification and reference SDK for the **`.uni` (v8.0 Universal)** non-executable semantic, telemetry, and cryptographic notary container.

The `.uni` format eliminates text-parsing overhead (`Zero-Parsing Inference`) and arbitrary code execution (`Zero-Execution Environment`) by packaging multidimensional floating-point tensors, atomic Knowledge Graph triplets, physical sensor telemetry, and `Ed25519` digital notary anchors into a single 32-byte-header binary container with per-node `AES-256-GCM` encryption and selective `Merkle Branch Proof` disclosure.

---

## Key Features (v8.0 Universal Baseline)

1. **$O(1)$ 32-Byte Hardware-Aligned Header (`UniHeader`):** Constant-time verification of packet integrity (`Blake2s-32`), 64-bit microsecond epoch timestamps, and exact payload byte limits (`PAYLOAD_LIMIT`) prior to dynamic memory allocation.
2. **Six Universal TLV Node Types:**
   * `0x01 NOTARY_ANCHOR` — 256-bit Merkle Root, `Ed25519` signature, $\Delta t$ cooling-off timelock, and steganographic `Duress Key` support.
   * `0x02 SEMANTIC_TENSOR` — Raw IEEE 754 `float32` vector embeddings for instant cosine similarity clustering.
   * `0x03 KNOWLEDGE_GRAPH` — Atomic `[Subject -> Predicate -> Object]` triplets with `ego_alignment` weights and Delta Conflict Superposition.
   * `0x04 TELEMETRY_MATRIX` — High-density binary sensor and medical screening matrices (`MZM-Pod` compatible).
   * `0x05 BEHAVIOR_CONTRACT` — Volatility timers (`TTL`), memory zone routing, and UI intent tags.
   * `0x06 GENESIS_TEXT` — Human-readable Markdown/UTF-8 fallback for legacy transcoding (DICOM, HL7 FHIR, PDF).
3. **Selective Zero-Knowledge Node Disclosure:** Derived per-node keys (`RFC 5869 HKDF-SHA256` + `AES-256-GCM`) allow the owner to decrypt and prove the authenticity of a single node to a third party via a SHA-256 `Merkle Branch Proof` while keeping all other nodes concealed.
4. **4-Zone Dynamic Memory Triage:** Automated routing across `Zone 0 (Sovereign Vault)`, `Zone 1 (Active Stream)`, `Zone 2 (Semantic Archive)`, and `Zone 3 (Quarantine)`.

---

## Quick Start

```bash
python3 reference/python/uni_core_sdk.py


