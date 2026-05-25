# ZK-based Proof of Personhood for Online Forum

This repo aims for exploring the PoC of ZK-based proof of personhood for BBS (Bulletin Board System) platforms. The tech is targeting for using [OpenAC](https://github.com/privacy-ethereum/zkID/blob/main/paper/zkID.pdf) and [its implementation from PSE's zkID team](https://github.com/privacy-ethereum/zkID/tree/main/wallet-unit-poc) to verify Taiwan's Citizenship Certificate.

## System Architecture for OpenAC Integration

### Proof Requirements

> One-time per credential proof for BBS server

- Verify the user holds a valid mobile citizenship certificate
    - no need extra check on age and nationalities since holding the certificate proves that
- Verify the mobile citizenship certificate has not been registered before

## Web-based Approach

> more common for both physical citizenship certificate (physical card) and mobile citizenship certificate (mobile app)

| ![mobile citizenship certificate for web app](/assets/web-flow-1.jpg) |
|:-:|
| *mobile citizenship certificate (mobile app)* |

| ![physical citizenship certificate for web app](/assets/web-flow-2.jpg) |
|:-:|
| *physical citizenship certificate (physical card), requires a card reader* |

### Flow
1. User → Issuer: apply mobile citizenship certificate
2. User → Web App: use API to fetch mobile citizenship certificate, and wrap it into JWT-format VC
3. Web App: Generate ZKP
4. Web App → BBS server: Submit ZKP with API
5. BBS server: verify ZKP
    - if pass, update user DB with `user.vcVerified = true`
    - if failed, update user DB with `user.vcVerified = failed`
### Frontend
- Fetch mobile citizenship certificate data with APIs
- Wrap raw data into JWT-format VC
- Generate ZKP using OpenAC
    - (OpenAC → wasm-bindgen → WASM)
- Send ZKP to BBS for verification
### Backend
- APIs for OpenAC proof verification on BBS server
    - Go, FFI can use https://github.com/ihciah/rust2go

## Mobile-based Approach

| ![mobile citizenship certificate for mobile app](/assets/mobile-flow.jpg) |
|:-:|
| *mobile citizenship certificate (mobile app)* |

### Flow
1. BBS mobile app → API to fetch mobile citizenship certificate and wrap it into JWT-format VC
2. within mobile app: generate ZKP (with mopro-ffi bindings)
3. mobile app → BBS server: submit ZKP with API
4. BBS server: verify ZKP
    - if pass, update user DB with `user.vcVerified = true`
    - if failed, update user DB with `user.vcVerified = failed`
### Frontend
> Integrate with existing official mobile app for specific BBS

- Fetch mobile citizenship certificate data with APIs
- Wrap raw data into JWT-format VC
- Generate ZKP using OpenAC with mopro-ffi bindings
- Send ZKP to BBS for verification

### Backend
- APIs for OpenAC proof verification on BBS server
    - feasibility check
        - Go, FFI can use https://github.com/ihciah/rust2go
