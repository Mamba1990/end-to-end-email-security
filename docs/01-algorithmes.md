# 01 – Algorithmes supportés par GnuPG

## Commande
```bash
gpg --version
```
Sortie complète : [`outputs/01-gpg-version.txt`](../outputs/01-gpg-version.txt)

**Environnement :** GnuPG 2.2.27, libgcrypt 1.9.4 (Ubuntu 22.04)

## Algorithmes asymétriques (Pubkey)
| Algorithme | ID OpenPGP | Usage |
|---|---|---|
| RSA | 1 | Signature **et** chiffrement |
| ELG (ElGamal) | 16 | Chiffrement uniquement |
| DSA | 17 | Signature uniquement |
| ECDH | 18 | Chiffrement (courbes elliptiques) |
| ECDSA | 19 | Signature (courbes elliptiques) |
| EdDSA | 22 | Signature (Ed25519) |

## Algorithmes symétriques (Cipher)
| Algorithme | ID OpenPGP | Taille de clé | Statut |
|---|---|---|---|
| IDEA | 1 | 128 bits | ⚠️ obsolète (blocs 64 bits) |
| 3DES | 2 | 168 bits | ⚠️ obsolète |
| CAST5 | 3 | 128 bits | ⚠️ obsolète |
| BLOWFISH | 4 | 128 bits | ⚠️ obsolète |
| AES / AES192 / AES256 | 7 / 8 / 9 | 128 / 192 / 256 bits | ✅ recommandé |
| TWOFISH | 10 | 256 bits | ✅ |
| CAMELLIA128 / 192 / 256 | 11 / 12 / 13 | 128 / 192 / 256 bits | ✅ |

## Fonctions de hachage (Hash)
| Algorithme | ID OpenPGP | Taille de l'empreinte | Statut |
|---|---|---|---|
| SHA1 | 2 | 160 bits | ⚠️ collisions démontrées (SHAttered, 2017) |
| RIPEMD160 | 3 | 160 bits | ⚠️ déconseillé |
| SHA256 | 8 | 256 bits | ✅ par défaut |
| SHA384 | 9 | 384 bits | ✅ |
| SHA512 | 10 | 512 bits | ✅ |
| SHA224 | 11 | 224 bits | ✅ |

## Compression
| Algorithme | ID OpenPGP |
|---|---|
| Uncompressed | 0 |
| ZIP | 1 |
| ZLIB | 2 |
| BZIP2 | 3 |

> Les ID OpenPGP (RFC 4880) réapparaîtront dans les étapes suivantes, par exemple
> `algo 1` (RSA) ou `digest algo 8` (SHA256) dans les sorties de `gpg --list-packets`.

## À retenir : PGP est un système hybride
1. **Compression** du message (ZLIB, par exemple).
2. **Chiffrement symétrique** du message avec une **clé de session** aléatoire (AES256, par exemple). C'est rapide, même pour un gros message.
3. **Chiffrement asymétrique** de la clé de session avec la **clé publique** de chaque destinataire (RSA, par exemple). Seul le destinataire peut la récupérer.
4. **Signature** : le message est **haché** (SHA256), puis l'empreinte est signée avec la **clé privée** de l'émetteur. Cela garantit l'intégrité, l'authentification et la non-répudiation.
