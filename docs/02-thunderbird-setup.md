# 02 – Configuration de Thunderbird avec Gmail

## Paramètres du compte
| Serveur | Protocole | Hôte | Port | Sécurité | Authentification |
|---|---|---|---|---|---|
| Entrant | IMAP | imap.gmail.com | 993 | SSL/TLS | OAuth2 |
| Sortant | SMTP | smtp.gmail.com | 465 | SSL/TLS | OAuth2 |

![Configuration manuelle](../captures/02-config-manuelle.png)

## Choix techniques
- **IMAP plutôt que POP3** : les mails restent sur le serveur Gmail, ce qui garde les messages de test synchronisés.
- **SSL/TLS** : la connexion entre Thunderbird et Gmail est chiffrée.
- **OAuth2** : Google délivre un jeton à Thunderbird. Le mot de passe du compte n'est jamais stocké localement, et l'accès peut être révoqué depuis le compte Google.

## Test d'envoi
Mail envoyé à ma propre adresse et reçu correctement :

![Mail de test reçu](../captures/02-mail-test.png)

## À retenir : TLS ≠ chiffrement de bout en bout
| | TLS | PGP / S/MIME |
|---|---|---|
| Protège | le transport (poste ↔ serveur) | le message lui-même |
| Mail stocké chez Gmail | **en clair** pour Google | **chiffré**, illisible par Google |
| Authentifie l'expéditeur | non | oui (signature) |

TLS est nécessaire, mais il ne suffit pas. Les étapes suivantes ajoutent la sécurité **de bout en bout** avec PGP puis S/MIME.
