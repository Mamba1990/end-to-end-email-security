# 🔐 End-to-End Email Security with OpenPGP and S/MIME

EFM project, supervised by Prof. Ahmed EL-YAHYAOUI.
Author: **Your Name**, Program/Year

## Objectives
Implement confidentiality, authentication, integrity and non-repudiation
for email using the IETF standards **OpenPGP** and **S/MIME**.

## Environment
| Component | Tool |
|---|---|
| OS | Ubuntu 22.04+ |
| Mail client | Thunderbird |
| OpenPGP | GnuPG |
| S/MIME | OpenSSL |

## Progress
- [x] 01 – Algorithms supported by GnuPG
- [ ] 02 – Thunderbird configuration
- [ ] 03 – PGP key pair generation and analysis
- [ ] 04 – PGP signed / encrypted emails
- [ ] 05 – PGP key exchange and certification
- [ ] 06 – PGP key revocation
- [ ] 07 – S/MIME key, CSR and X.509 certificate
- [ ] 08 – S/MIME signed / encrypted emails

## Repository layout
| Folder | Content |
|---|---|
| `docs/` | Report for each step |
| `outputs/` | Raw command outputs |
| `captures/` | Screenshots |
| `pgp/` | Public PGP keys, saved .eml emails |
| `smime/` | CSR and public certificates |

> ⚠️ No private key is published in this repository (see `.gitignore`).
