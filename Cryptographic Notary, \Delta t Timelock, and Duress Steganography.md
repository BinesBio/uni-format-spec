Cryptographic Notary, \Delta t Timelock, and Duress Steganography
To replace bureaucratic notarization while safeguarding human agency, Node 0
(NOTARY_ANCHOR) implements three cryptographic mechanisms: Two-Phase Cooling-Off Timelock (\Delta t Validation): For high-stakes legal, financial, or medical
consents, cooling_off_delta_t_sec specifies a mandatory time gradient \Delta t > 0 (e.g., 43,200
seconds / 12 hours). Initial signing places the container in
PENDING_DELTA_T_CONFIRMATION. Finalization requires a second cryptographic signature
after T_0 + \Delta t, preventing impulsive decisions made under acute emotional affect (\Delta t
< \text{minutes}).
Dual-Key Duress Steganography (Primary vs. Duress Ed25519 Keys): The user's sovereign key
vault (Zone 0) maintains two distinct Ed25519 keypairs: a Primary Keypair (unlocked via normal
authentication) and a Duress Keypair (unlocked via a coercion PIN/gesture).
If coerced by an attacker, the user signs with the Duress Key.
External Indistinguishability: Standard public signature verification checks math validity against
the signer public key embedded in Node 0 and returns True (VALID). The coercer sees no
warning flags on screen.
Silent Quarantine Routing: When the container reaches the user's personal cloud node or a
trusted syndicate registry that recognizes the Duress Public Key, the node silently routes the
container into Zone 3 (Quarantine) and invalidates execution.
Unidirectional Optical Transport & FEC: For air-gapped hardware (such as the MZM-Pod), the
.uni container is appended with Reed-Solomon RS(255, 223) forward error correction parity
blocks, enabling 100% single-pass recovery over a unidirectional optical data diode without
ACK/NACK feedback channels.
