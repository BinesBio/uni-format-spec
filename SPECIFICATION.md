# `.uni` (Universal Neural Interface / Universal Node Identity) Format Specification
**Version:** 8.0.0 (Universal Reality-Verified Baseline)  
**Status:** Open Standard Specification & Prior Art Baseline  
**License:** Uni-Symbiosis Public License v1.0 (USPL-1.0) / CC-BY-4.0  

---

## 1. Architectural Overview & Core Principles

Traditional document and serialization formats (PDF, DOCX, HTML, JSON) are designed for human visual rendering or verbose text parsing, forcing AI systems and edge processors to waste computational resources translating character streams into multidimensional vectors.

The **`.uni`** standard eliminates this bottleneck by operating as a binary-serialized, non-executable semantic and telemetry container engineered for direct tensor operations, granular cryptographic disclosure, and automated cryptographic notarization.

### Fundamental Design Guarantees
1. **Zero-Parsing Inference:** Native storage of IEEE 754 floating-point embeddings (`float32` tensors) and atomic Knowledge Graph triplets (`[Subject] -> [Predicate] -> [Object]`) enables immediate vector similarity comparison and graph traversal without text parsing.
2. **Zero-Execution Environment:** The `.uni` container is strictly a passive data structure incapable of housing executable binary opcodes, macros, or arbitrary scripts. Incoming streams are validated at the buffer boundary via strict Type-Length-Value (TLV) schema enforcement (`sterile_ingest`), reducing the code-execution attack surface to zero.
3. **Dual-Layer Genesis Envelope (Backward Compatibility):** A single `.uni` container simultaneously supports modern AI accelerators (via binary tensor nodes) and legacy systems (via a human-readable Markdown/UTF-8 node or deterministic transcoding into DICOM, HL7 FHIR, and PDF).
4. **Granular Per-Node Encryption & Selective Disclosure:** Each internal node is encrypted independently using `AES-256-GCM` with keys derived via `RFC 5869 HKDF-SHA256` and bound via a SHA-256 Merkle Tree. The container owner can disclose and mathematically prove the authenticity of a single node (e.g., for a medical specialist or external auditor) via a `Merkle Branch Proof` without exposing any other nodes in the file.
5. **Cryptographic Notary & Anti-Coercion Layer:** Built-in `Ed25519` digital signatures, a 64-bit microsecond timestamp, a two-phase cooling-off timelock ($\Delta t$), and dual-key steganographic duress detection (`Primary Key` vs. `Duress Key`) replace paper notarization while protecting the human host against coercion and impulsive affect.

---

## 2. Binary Container Topology & 32-Byte $O(1)$ Header (`UniHeader`)

Every `.uni` v8.0 file begins with a fixed **32-byte AVX2-aligned header** encoded in Little-Endian byte order (`<4sHHIIQ4s4s`). Network controllers (SmartNIC/eBPF) and optical data-diode buffers validate this header in $O(1)$ constant time prior to dynamic heap allocation.

```text
+-----------------------------------------------------------------------+
| 0x00 - 0x03 (4B) | MAGIC_BYTES   : ASCII "UNI8" (0x55 0x4E 0x49 0x38) |
+-----------------------------------------------------------------------+
| 0x04 - 0x05 (2B) | PROTO_FLAGS   : Version (0x0800) & Mode Bitmask    |
+-----------------------------------------------------------------------+
| 0x06 - 0x07 (2B) | NODE_BITMAP   : 16-bit Active Node Presence Mask   |
+-----------------------------------------------------------------------+
| 0x08 - 0x0B (4B) | PAYLOAD_LIMIT : Exact Payload Size in Bytes (uint32)|
+-----------------------------------------------------------------------+
| 0x0C - 0x0F (4B) | SESSION_SALT  : 32-bit Hardware TRNG Entropy Salt  |
+-----------------------------------------------------------------------+
| 0x10 - 0x17 (8B) | TIMESTAMP_US  : 64-bit Microsecond Epoch Counter   |
+-----------------------------------------------------------------------+
| 0x18 - 0x1B (4B) | MERKLE_TAG    : Truncated 32-bit Root Hash Anchor  |
+-----------------------------------------------------------------------+
| 0x1C - 0x1F (4B) | HEADER_ECC    : 32-bit Blake2s/CRC32 Header Check  |
+-----------------------------------------------------------------------+
| 0x20 - End       | Encrypted TLV Node Stream + Optional RS(255,223)   |
+-----------------------------------------------------------------------+



+-----------------------------------------------------------------------+
|  0x00 - 0x1F  | Chiral Lock Header (32 B) — O(1) Hardware Lock        |
+-----------------------------------------------------------------------+
|  0x20 - 0x5F  | Node Metadata & Snapshot (64 B) — V0 State & RS(64,48)|
+-----------------------------------------------------------------------+
|  0x60 - End   | Dual-Strand Tensor Payload                            |
|               |  - Strand Alpha: Direct tensor D_alpha                |
|               |  - Strand Beta:  Complementary tensor D_beta          |
+-----------------------------------------------------------------------+

1.1 Chiral Header Layout (32 Bytes)
Designed for single-cycle execution at the SmartNIC/eBPF boundary.
| Offset (Bytes) | Field Identifier | Size | Mathematical Specification |
|---|---|---|---|
| 0x00 - 0x03 | HOST_HASH | 4 B | H_{host} = \text{Truncate}_{32}(\text{SHA256}(V_0)) |
| 0x04 - 0x07 | CHIRAL_ORIENT | 4 B | \mathbf{T}_L = \mathbf{M}_{MD5}(H_{host} \parallel \text{ID}_{gateway}) \oplus \mathbf{0xAA} |
| 0x08 - 0x0F | TEMPORAL_NONCE | 8 B | 64-bit microsecond epoch timestamp (Mitigates Y2K38 & Replay attacks) |
| 0x10 - 0x13 | PARITY_LOCK | 4 B | P_{lock} = \text{Truncate}_{32}(\text{SHA256}(H_{host} \parallel \mathbf{T}_L \parallel \text{Nonce})) |
| 0x14 - 0x17 | TENSOR_DIM | 4 B | Exact payload size in bytes. Hardware drop triggers upon overflow. |
| 0x18 - 0x19 | MODE_FLAGS | 2 B | Routing and sandbox isolation flags. |
| 0x1A - 0x1F | RESERVED | 6 B | Reserved space for post-quantum lattice extensions. |
1.2 Cognitive Snapshot & Reed-Solomon Correction
The host's biological vector state (V_0) is immutable and requires physical decay protection before the inverse tensor operator can be applied.
 * 0x20 - 0x4F (48 Bytes): Raw Vector State (V_0).
 * 0x50 - 0x5F (16 Bytes): Reed-Solomon Error Correction Code \text{RS}(64,48).
 * Function: Guarantees on-the-fly reconstruction of up to 8 degraded bytes within the cognitive footprint, eliminating hallucinatory data unpacking during signal loss.
2. Validation & Dissipation Pipeline
Data passing the O(1) Chiral Lock enters a deterministic 5-stage ontological pipeline.
Stage 1: The Teleological Gateway (Thermodynamic Dissipation)
Information must possess applied utility to the active host state.
 * The tensor graph is rapidly unfolded to extract core semantic intent.
 * If the data fails to align with the host's active focus or operational matrix (V_0), it is subjected to Thermodynamic Dissipation—dropped from memory prior to execution.
 * Result: Spam, cognitive pressure arrays, and logic bombs are starved of ontological gas without consuming heavy simulation cycles.
Stage 2: Cognitive Pressure Filter
Scans for neuro-linguistic coercion, behavioral forcing vectors, or non-disclosed manipulation embedded within utility-approved data.
Stage 3: Topological & Logical Coherence
Verifies internal mathematical consistency. Abstract noise, paradoxical loops, and self-referential hallucinations are rejected strictly on the basis of pure formal logic, independent of physical laws.
Stage 4: Physics Simulation Sandbox
Mathematically coherent data that contradicts known physical paradigms is isolated in an isometric simulation chamber.
 * If the construct collapses under causal testing \rightarrow Tagged as Error.
 * If the construct maintains causal integrity \rightarrow Classified as a "Black Swan" (\mathcal{S}_{swan}) and integrated to expand the global ontology.
Stage 5: Zero-Trust Empathy Buffer
Authorized data is injected into the host's runtime via a metered delivery rate matching the psychophysiological feedback loop of V_0.
3. Dual-Strand Tensor Payload
The payload consists of two mutually dependent tensor strands to detect mid-transit bit-rot or active forgery:
Upon localized physical degradation of the primary strand, reconstruction occurs via the inverse operator, mathematically shielded by the RS-corrected V_0 state:
Published under the Uni-Symbiosis Public License v1.0 (USPL-1.0).

