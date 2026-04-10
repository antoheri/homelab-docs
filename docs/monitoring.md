# Stack Monitoring

## Architecture

```
┌─────────────────────────────────────────┐
│              Grafana                    │
│         (Visualisation)                 │
└──────────────┬──────────────────────────┘
               │
       ┌───────┴────────┐
       │                │
┌──────▼──────┐  ┌──────▼──────┐
│ Prometheus  │  │  Pi-hole    │
│ (Métriques) │  │   (API)     │
└──────┬──────┘  └─────────────┘
       │
┌──────▼──────────────────────────────────┐
│            Exporters                    │
│  - Node Exporter (système)              │
│  - cAdvisor (Docker)                    │
│  - Blackbox (ping/dns)                  │
└─────────────────────────────────────────┘
```

## Composants

### Prometheus

**Rôle :** Collecte et stockage time-series

- Scraping toutes les 15s
- Rétention 15 jours
- Alertmanager pour notifications

### Grafana

**Rôle :** Dashboards et alertes visuelles

- Dashboards custom
- Alertes par email/Telegram
- Authentification basique

### Exporters

| Exporter | Métriques |
|----------|-----------|
| Node Exporter | CPU, RAM, disque, réseau |
| cAdvisor | Containers Docker (CPU, mémoire, I/O) |
| Blackbox | Latence, disponibilité services |

## Dashboards

### Node Overview
- Utilisation CPU/RAM
- Espace disque
- Charge système
- Uptime

### Docker Containers
- CPU par container
- Utilisation mémoire
- Status up/down
- Restart count

### Pi-hole Statistics
- Requêtes DNS totales
- Requêtes bloquées
- Top blocked domains
- Clients actifs

## Alertes configurées

| Condition | Seuil | Action |
|-----------|-------|--------|
| Disk full | > 85% | Alert |
| Memory high | > 90% | Alert |
| Service down | 0 | Alert |
| Backup fail | - | Alert |

---
*Stack complète, prête pour production homelab.*
