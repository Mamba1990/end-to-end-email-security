# 01 – Algorithms Supported by GnuPG

## Command
```bash
gpg --version
```
Full output: [`outputs/01-gpg-version.txt`](../outputs/01-gpg-version.txt)

**Environment:** GnuPG 2.2.27, libgcrypt 1.9.4 (Ubuntu 22.04)

## Asymmetric algorithms (Pubkey)
| Algorithm | OpenPGP ID | Use |
|---|---|---|
| RSA | 1 | Signing **and** encryption |
| ELG (ElGamal) | 16 | Encryption only |
| DSA | 17 | Signing only |
| ECDH | 18 | Encryption (elliptic curves) |
| ECDSA | 19 | Signing (elliptic curves) |
| EdDSA | 22 | Signing (Ed25519) |

## Symmetric algorithms (Cipher)
| Algorithm | OpenPGP ID | Key size | Status |
|---|---|---|---|
| IDEA | 1 | 128 bits | ⚠️ obsolete (64-bit blocks) |
| 3DES | 2 | 168 bits | ⚠️ obsolete |
| CAST5 | 3 | 128 bits | ⚠️ obsolete |
| BLOWFISH | 4 | 128 bits | ⚠️ obsolete |
| AES / AES192 / AES256 | 7 / 8 / 9 | 128 / 192 / 256 bits | ✅ recommended |
| TWOFISH | 10 | 256 bits | ✅ |
| CAMELLIA128 / 192 / 256 | 11 / 12 / 13 | 128 / 192 / 256 bits | ✅ |

## Hash functions
| Algorithm | OpenPGP ID | Digest size | Status |
|---|---|---|---|
| SHA1 | 2 | 160 bits | ⚠️ practical collisions (SHAttered, 2017) |
| RIPEMD160 | 3 | 160 bits | ⚠️ not recommended |
| SHA256 | 8 | 256 bits | ✅ default |
| SHA384 | 9 | 384 bits | ✅ |
| SHA512 | 10 | 512 bits | ✅ |
| SHA224 | 11 | 224 bits | ✅ |

## Compression
| Algorithm | OpenPGP ID |
|---|---|
| Uncompressed | 0 |
| ZIP | 1 |
| ZLIB | 2 |
| BZIP2 | 3 |

> The OpenPGP IDs (RFC 4880) appear again in later steps, for example
> `algo 1` (RSA) or `digest algo 8` (SHA256) in `gpg --list-packets` output.

## Key takeaway: PGP is a hybrid system
1. **Compression** of the message (e.g. ZLIB).
2. **Symmetric encryption** of the message with a random **session key** (e.g. AES256). This is fast, even for large messages.
3. **Asymmetric encryption** of the session key with each recipient's **public key** (e.g. RSA). Only the recipient can recover it.
4. **Signature**: the message is **hashed** (SHA256), and the digest is signed with the sender's **private key**. This provides integrity, authentication and non-repudiation.
