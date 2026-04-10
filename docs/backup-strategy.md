# Stratégie de Backup

## Vue d'ensemble

Système de backup 3-2-1 simplifié :
- **3** copies des données importantes
- **2** types de stockage différents

## Outil : BorgBackup

### Pourquoi Borg ?

- **Déduplication** : économie d'espace
- **Compression** : ZSTD par défaut
- **Chiffrement** : AES-256
- **Détection corruption** : checksums

### Architecture

```
Source              │    Borg    │    Destination
────────────────────┼────────────┼────────────────
/etc/               │   create   │  /backups/
/home/              │   prune    │  (USB 2TB)
Docker volumes      │   check    │
```

### Workflow

```bash
# 1. Backup quotidien
borg create ::{now} /etc /home /var/lib/docker/volumes

# 2. Rotation (garder 7 daily, 4 weekly, 6 monthly)
borg prune --keep-daily=7 --keep-weekly=4 --keep-monthly=6

# 3. Vérification intégrité
borg check
```

### Récupération

```bash
# Liste backups
borg list /mnt/backup

# Extraction
borg extract /mnt/backup::2024-04-10 /home/user/document

# Montage FUSE (parcourir)
borg mount /mnt/backup::2024-04-10 /mnt/tmp
```

## Automatisation

- **Systemd timer** : lancement quotidien 2h du matin
- **Notifications** : alerte si échec
- **Monitoring** : export métriques (taille, durée, statut)

## Scripts

- `backup.sh` : wrapper avec logging
- `restore.sh` : procédure interactive
- `check.sh` : vérification intégrité

---
*Détails d'implémentation disponibles sur demande.*
