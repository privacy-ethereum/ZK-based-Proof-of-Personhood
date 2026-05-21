# ZK-based Human Verification

A proof-of-concept for ZK-based human verification on BBS (Bulletin Board System) platforms using [OpenAC](https://github.com/privacy-ethereum/zkID/blob/main/paper/zkID.pdf) and Taiwan's Citizenship Certificate.

> For system design, flow diagrams, and architecture decisions, see [ARCHITECTURE.md](./ARCHITECTURE.md).

## Repository Structure

```
.
├── zkid/                    # ZK identity core — circuit and proof logic (mopro-based)
├── go-zkid-verifier/        # Go server-side verifier for OpenAC ZK proofs
├── moica-revocation-smt/    # Sparse Merkle Tree for MOICA certificate revocation checks
├── OpenACSwift/             # iOS Swift bindings for OpenAC proof generation
├── OpenACKotlin/            # Android Kotlin bindings for OpenAC proof generation
└── assets/                  # Architecture diagrams
```

## Submodules

| Module | Role |
|--------|------|
| [zkid](https://github.com/zkmopro/zkid) | ZK circuit and proof generation core, built with mopro |
| [go-zkid-verifier](https://github.com/zkmopro/go-zkid-verifier) | Backend verifier exposing Go APIs for BBS servers to verify OpenAC proofs |
| [moica-revocation-smt](https://github.com/moven0831/moica-revocation-smt) | SMT-based revocation registry for MOICA certificates |
| [OpenACSwift](https://github.com/zkmopro/OpenACSwift) | Swift package wrapping OpenAC FFI bindings for iOS |
| [OpenACKotlin](https://github.com/zkmopro/OpenACKotlin) | Kotlin library wrapping OpenAC FFI bindings for Android |

## Getting Started

Clone with all submodules:

```bash
git clone --recurse-submodules https://github.com/YOUR_ORG/ZK-based-Human-Verification.git
```

If already cloned:

```bash
git submodule update --init --recursive
```
