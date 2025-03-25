---
title: Storage Backend Issue Causing Unavailability
date: 2025-03-25 15:17:47
resolved: true
resolvedWhen: 2025-03-25 17:16:52
severity: down
affected:
  - BookStack
  - Cyber Range
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

Our storage backend accrued several I/O timeouts, resulting in it automatically suspending itself and causing unavailability across the CNS network. Rebooting the server resulted in the restoration of all functionality.

*Resolved* - All service has been restored. {{< track "2025-03-25 17:16:52" >}}

*Investigating* - We are investigating the issue. {{< track "2025-03-25 15:17:47" >}}
