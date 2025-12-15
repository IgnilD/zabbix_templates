This template is for Zabbix version: 7.0

# Zabbix Template: DELL PowerProtect DataDomain SNMP

## Overview

This Zabbix template provides comprehensive monitoring for **Dell PowerProtect Data Domain** (formerly EMC Data Domain) appliances via SNMP.

## Requirements:
Zabbix version: 7.0 and higher.

## Configuration

Zabbix should be configured according to the instructions in the [Templates out of the box](https://www.zabbix.com/documentation/7.4/en/manual/config/templates_out_of_the_box) section.

## Setup
1. Create a host for DataDomain with management IP as SNMP interface.
2. Link the template to the host.
3. Customize macro values if needed.



### Static Items
- System information (model, serial number, version, uptime, notes, contact, location, name)
- CPU usage (average and max busy %)
- Disk busy, read, and write rates
- File system status and message
- DDBoost backup/restore connections
- CIFS and NFS operations rate
- SNMP agent availability check
- Fallback SNMP trap catcher

### Discovery Rules & Prototypes
1. **Network Interfaces** – Standard IF-MIB discovery with traffic, errors, discards, speed, status, and triggers for link down, high utilization, high error rate, speed changes.
2. **Disks** – Discovers individual disks per enclosure with model, serial, firmware, capacity, state, and triggers for failed/absent/unknown disks and reconstruction events.
3. **Enclosures** – Model, serial, capacity.
4. **Fans** – Per-enclosure fan description, speed level, status with critical triggers.
5. **Power Supplies (PSU)** – Per-enclosure PSU status with critical/warning triggers.
6. **Temperature Sensors** – Per-enclosure sensor description, current value (°C), status with overheat and failure triggers.
7. **NVRAM** – Memory size, PCI/memory error counts, and per-battery charge/status with low charge and failure triggers.
8. **NVRAM BBU** – Battery charge and status monitoring.
9. **File Systems** – Per-resource (name + tier) space used/available/cleanable/size and triggers for high utilization (85% warning, 95% critical).
10. **DDBoost Interfaces** – Backup, restore, and total connections per interface (discovery currently disabled by default).
11. **Ports** – Physical port link speed changes.

### Triggers
- Host restart detection (uptime < 10 min)
- File system not in optimal state
- Device replacement (serial number change)
- System version change
- System name change
- Component-specific failures (disks, fans, PSUs, temperature, NVRAM batteries, etc.)
- Performance alerts (high CPU/disk/network utilization, errors)

### Tags
- `class: hardware`
- `target: data domain`, `dell`, `power protect`
- Component-specific tags (e.g., `component: filesystem`, `component: disk`, `component: fan`)

### Macros
Standard macros for thresholds and filters (e.g., `{$FS.SPACE.WARN}=85`, `{$FS.SPACE.CRIT}=95`, network interface filters, etc.) – all customizable per host/template.

## Installation

1. In Zabbix frontend, go to **Configuration → Templates**.
2. Click **Import** in the upper right.
3. Select the YAML file containing this template (or paste the content if importing manually).
4. Confirm import (enable "Create new" for groups if needed).
5. Assign the template **DELL PowerProtect DataDomain SNMP** to your Data Domain hosts.
6. Configure SNMP on the Data Domain device (community string, usually `public` for read-only).
7. Wait for discovery (most rules run every 1 hour, temperature every 10 min).

## Customization Tips

- Adjust filesystem thresholds via macros `{$FS.SPACE.WARN}` and `{$FS.SPACE.CRIT}` on host or template level.
- Fine-tune network interface discovery filters if needed (default excludes loopbacks, docker interfaces, etc.).
- Enable the disabled **DDBoost Connections discovery** rule if you want per-interface DDBoost metrics.
- Use host macros to override any component-specific thresholds (e.g., NVRAM battery low charge warning).

## Known Notes

- Some items use `DISCARD_UNCHANGED_HEARTBEAT` to reduce stored values for rarely changing data (serial, model, firmware, etc.).
- Units are properly converted (e.g., disk rates from KB/s → B/s, filesystem GB → bytes).
- Triggers include manual close option where appropriate.

Enjoy reliable monitoring of your Dell PowerProtect Data Domain appliances!
