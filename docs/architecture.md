# Architecture Homelab

## Vue d'ensemble

Infrastructure personnelle conçue pour :
- Apprentissage DevOps/Infrastructure
- Démonstration de compétences
- Services personnels utiles (DNS, monitoring, backup)

## Composants

### 1. Node Edge (Raspberry Pi)

**Rôle :** Services réseau et edge computing

| Service | Fonction | Technologie |
|---------|----------|-------------|
| Pi-hole | DNS + filtrage | Docker |
| Prometheus | Collecte métriques | Docker |
| Grafana | Visualisation | Docker |
| Node Exporter | Métriques système | Docker |
| BorgBackup | Sauvegardes | Natif |

### 2. Workstation (Contrôleur)

**Rôle :** Management et développement

- Ansible (Configuration Management)
- Git (Versionning)
- Docker (Build images)

## Flux de données

```
Internet ◄──► Pi-hole (filtrage) ◄──► LAN
                │
                ▼
           Prometheus ◄──► Grafana (dashboards)
                │
                ▼
           BorgBackup (archives chiffrées)
```

## Sécurité

- SSH clé uniquement (pas de password)
- Containers isolés
- Backup chiffré (repo-key)
- Pas de services exposés sur WAN

## Monitoring

Métriques collectées :
- CPU, RAM, disque (Node Exporter)
- Statistiques DNS (Pi-hole API)
- Docker containers (cAdvisor)
- Alertes disponibles

## Backup Strategy

| Source | Destination | Fréquence | Rétention |
|--------|-------------|-----------|-----------|
| Configs | NAS externe | Quotidien | 30 jours |
| Docker volumes | NAS externe | Quotidien | 30 jours |

---
*Architecture évolutive, documentée as-code.*
