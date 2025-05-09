---
title: Infrastructure Storage Backend Failure
date: 2025-03-16 12:07:12
resolved: true
resolvedWhen: 2025-03-18 12:13:49
severity: down
affected:
  - BookStack
  - CyberStorm Website
  - Keycloak
  - LibreNMS
  - Netbox
  - Network Builder
  - Proxmox
  - Wazuh
  - Website
  - VPN
  - HSPC
  - Megafonzie
section: issue
---

**Update:** The backend has been rebuilt. No data has been lost and all functionality has been restored.

The server hosting the CNS infrastructure storage backend appears to have suffered unexpected power loss. Upon restarting, a hard drive failed.
The backend is currently rebuilding and no data loss is expected at this time, but access to CNS services is unavailable until the rebuild is complete. {{< track "2025-03-16 12:07:12" >}}
