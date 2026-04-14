
                👤 Users
                    │
        Azure Front Door
                    │
                 WAF
                    │
        ┌───────────────────────────────┐
        │   Azure Virtual Network       │
        │       (Multi-AZ)              │
        │                               │
        │  ┌──────── Public Subnet ───┐ │
        │  │                          │ │
        │  │   (Entry handled above)  │ │
        │  └──────────────────────────┘ │
        │                               │
        │  ┌──── Private Subnet ──────┐ │
        │  │                          │ │
        │  │      AKS Cluster         │ │
        │  │   (API + Worker Pods)    │ │
        │  │   Auto Scaling Enabled   │ │
        │  └──────────────────────────┘ │
        │                               │
        │  ┌──── Database Subnet ─────┐ │
        │  │                          │ │
        │  │   PostgreSQL (Primary)   │ │
        │  │   PostgreSQL (Replica)   │ │
        │  │   Redis Cache            │ │
        │  └──────────────────────────┘ │
        │                               │
        └───────────────────────────────┘

              │                │
              │                │
      Azure Key Vault     Azure Monitor
      Azure AD            Log Analytics

              │
      Secondary Region (DR)
