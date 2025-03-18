---
title: Infrastructure Hard Drive Failure
date: 2025-03-18 12:24:54
informational: true
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

## Summary

A hard drive in the RAID array backing CNS infrastructure began behaving abnormally, degrading performance on all CNS services to unusable levels. The drive was replaced and the RAID setup rebuilt itself.

## Timeline

*All times are in Eastern Daylight Time (UTC-04:00).*

* March 16, 12:07 PM: `zfs1`, our infrastructure storage server, reboots. The cause of the reboot is unknown, but believed to be the result of temporary power loss due to the weather. At this time, the hard drive in bay 3 fails.
* March 16, 2:53 PM: The issue is first noticed as VPN unavailability, but mistakenly attributed to an issue with the user's network.
* March 16, 7:26 PM: The issue is identified as residing with CNS infrastructure.
* March 16, 8:06 PM: The Proxmox servers are determined to be online, but the VMs on them are experiencing issues.
* March 16, 8:27 PM: The root cause is preliminarily attributed to `delphox` and `beheeyem`, the CNS domain controllers.
* March 16, 9:07 PM: Remote access to the network is obtained for the first time since the outage began.
* March 16, 11:06 PM: The root cause is identified as a storage issue.
* March 17, 12:32 AM: BookStack is restored from a backup and hosted on a cloud server. It is the only service to be restored in this manner during the outage.
* March 17, 9:52 AM: The root cause is identified as a failed drive in the RAID array.
* March 17, 11:27 AM: `zfs1` is rebooted in an attempt to start the RAID rebuild process using a hot spare.
* March 18, 10:40 PM: The RAID array has not actually begun rebuilding, so `zfs1` is rebooted again.
* March 18, 8:54 AM: The RAID array has finished rebuilding itself. `zfs1` is started into the operating system.
* March 18, 11:00 AM: The failed drive is replaced with a working drive.
* March 18, 11:56 AM: The RAID array is deemed fully operational.
* March 18, 12:06 PM: The storage backend is deemed fully healthy.
* March 18, 12:13 PM: All affected services are determined to be functional, concluding the incident.

## Root Cause

The sudden power loss caused one of the disks in the RAID array to exhibit SMART errors and behave erratically. The degraded performance made the entire array unusable, resulting in all the services becoming unavailable.

## Resolution

The array uses RAID 5, which can rebuild from single-drive failures. It was rebuilt using a hot-spare already installed in the array. Afterwards, the failed drive was replaced with a working one in order to prevent the failed drive from being used further.

## Corrective and Preventative Measures

This incident served as a reminder of the instability of our storage backend, which relies on one server and storage array in order to power all CNS operations. We will be investigating the storage backend in order to improve its reliability in the future.

Additionally, this incident highlighted the need for better backups of our core infrastructure. While we were able to restore BookStack from a backup, most of our other infrastructure -- including our domain configuration and network inventory -- is not backed up offsite. This meant we had to hope for a successful recovery or else we stood to lose important data. Going forward, we will focus on improving our disaster recovery procedures, including taking regular backups.
