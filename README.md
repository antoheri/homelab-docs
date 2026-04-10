# Homelab Infrastructure

Infrastructure personnelle de type "homelab" pour apprentissage DevOps et démonstration de compétences.

## Vue d'ensemble

```
┌─────────────────┐         ┌─────────────────┐
│   WORKSTATION   │  SSH    │   RASPBERRY PI  │
│   (Ansible)     │ ───────►│   (Edge Node)   │
│                 │         │                 │
│  - Ansible      │         │  - Pi-hole      │
│  - Playbooks    │         │  - Monitoring   │
│  - Git          │         │  - Backups      │
└─────────────────┘         └─────────────────┘
         │
         ▼
    GitHub (IaC versioning)
```

## Services déployés

| Service | Technologie | Rôle |
|---------|-------------|------|
| DNS interne | Pi-hole | Filtrage + stats DNS |
| Monitoring | Prometheus + Grafana | Métriques système |
| Backup | BorgBackup | Sauvegardes chiffrées |
| Orchestration | Ansible | Déploiement automatisé |

## Technologies

- **Ansible** — Configuration Management
- **Docker** — Conteneurisation
- **Prometheus/Grafana** — Observabilité
- **BorgBackup** — Backup dédupliqué
- **Pi-hole** — DNS sinkhole

## Architecture

![Architecture](docs/architecture.png)

*Schéma réseau simplifié. Configuration réelle disponible sur demande.*

## Ressources

- [Documentation technique](docs/)
- [Procédures de backup](docs/backup-strategy.md)
- [Monitoring stack](docs/monitoring.md)

## Contact

Configuration détaillée et accès aux playbooks réels disponibles sur demande pour recrutement.

---
*Infrastructure gérée as-code avec Ansible et Docker.*
