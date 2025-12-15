This template is for Zabbix version: 7.0

# Zabbix Template: DELL PowerProtect DataDomain by SNMP

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

## Macros used
These macros allow customization of thresholds and discovery filters. You can override them at the host or linked template level in Zabbix.

| Name | Description | Default Value |
|------|-------------|---------------|
| `{$DISK.STATUS.CRIT:"absent"}` | <p>The critical value of the Disk state for trigger expression.</p> | `3` |
| `{$DISK.STATUS.CRIT:"failed"}` | <p>The critical value of the Disk state for trigger expression.</p> | `4` |
| `{$DISK.STATUS.CRIT:"unknown"}` | <p>The critical value of the Disk state for trigger expression.</p> | `2` |
| `{$DISK.STATUS.INFO:"copyReconstruction"}` | <p>The informational value of the Disk state for trigger expression.</p> | `9` |
| `{$DISK.STATUS.INFO:"raidReconstruction"}` | <p>The informational value of the Disk state for trigger expression.</p> | `8` |
| `{$FAN.STATUS.CRIT:"fail"}` | <p>The critical value of the FAN sensor for trigger expression.</p> | `2` |
| `{$FAN.STATUS.CRIT:"notfound"}` | <p>The critical value of the FAN sensor for trigger expression.</p> | `0` |
| `{$FS.SPACE.CRIT}` | <p>The critical value of the Filesystem space used (in %) for trigger expression.</p> | `95` |
| `{$FS.SPACE.TIME}` | <p>The time during which Filesystem space usage may exceed the threshold.</p> | `10m` |
| `{$FS.SPACE.WARN}` | <p>The warning value of the Filesystem space used (in %) for trigger expression.</p> | `85` |
| `{$NET.IF.IFADMINSTATUS.MATCHES}` | <p>Ignore notPresent(6)</p> | `^.*` |
| `{$NET.IF.IFADMINSTATUS.NOT_MATCHES}` | <p>Ignore down(2) administrative status</p> | `^2$` |
| `{$NET.IF.IFALIAS.MATCHES}` |  | `.*` |
| `{$NET.IF.IFALIAS.NOT_MATCHES}` |  | `CHANGE_IF_NEEDED` |
| `{$NET.IF.IFDESCR.MATCHES}` |  | `.*` |
| `{$NET.IF.IFDESCR.NOT_MATCHES}` |  | `CHANGE_IF_NEEDED` |
| `{$NET.IF.IFNAME.MATCHES}` |  | `^.*$` |
| `{$NET.IF.IFNAME.NOT_MATCHES}` | <p>Filter out loopbacks, nulls, docker veth links and docker0 bridge by default</p> | `(^Software Loopback Interface|^NULL[0-9.]*$|^[Ll]o[0-9.]*$|^[Ss]ystem$|^Nu[0-9.]*$|^veth[0-9a-z]+$|docker[0-9]+|br-[a-z0-9]{12})` |
| `{$NET.IF.IFOPERSTATUS.MATCHES}` |  | `^.*$` |
| `{$NET.IF.IFOPERSTATUS.NOT_MATCHES}` | <p>Ignore notPresent(6)</p> | `^6$` |
| `{$NET.IF.IFTYPE.MATCHES}` |  | `.*` |
| `{$NET.IF.IFTYPE.NOT_MATCHES}` |  | `CHANGE_IF_NEEDED` |
| `{$NVRAM.BATTERY.CHARGE.WARN}` | <p>The warning value of the nvram battery for trigger expression.</p> | `50` |
| `{$NVRAM.BATTERY.STATUS.CRIT}` | <p>The critical status of the nvram battery for trigger expression.</p> | `2` |
| `{$NVRAM.BATTERY.STATUS.OK}` | <p>The OK status of the nvram battery for trigger expression.</p> | `0` |
| `{$NVRAM.BATTERY.STATUS.WARN:"disabled"}` | <p>The WARN status of the nvram battery for trigger expression.</p> | `1` |
| `{$NVRAM.BATTERY.STATUS.WARN:"softdisabled"}` | <p>The WARN status of the nvram battery for trigger expression.</p> | `3` |
| `{$PSU.STATUS.CRIT:"acnone"}` | <p>The critical value of the PSU sensor for trigger expression.</p> | `4` |
| `{$PSU.STATUS.CRIT:"failed"}` | <p>The critical value of the PSU sensor for trigger expression.</p> | `2` |
| `{$PSU.STATUS.CRIT:"faulty"}` | <p>The critical value of the PSU sensor for trigger expression.</p> | `3` |
| `{$PSU.STATUS.WARN:"absent"}` | <p>The warning value of the PSU sensor for trigger expression.</p> | `0` |
| `{$PSU.STATUS.WARN:"unknown"}` | <p>The warning value of the PSU sensor for trigger expression.</p> | `99` |
| `{$TEMP.SENSOR.ENCLOSURE.MATCHES}` | <p>Filter for discovering a temperature sensor by enclosure ID.</p> | `.*` |
| `{$TEMP.SENSOR.ENCLOSURE.NOT_MATCHES}` | <p>Filter for discovering a temperature sensor by enclosure ID.</p> | `CHANGE_IF_NEEDED` |
| `{$TEMP.SENSOR.STATUS.CRIT:"failed"}` | <p>The critical value of the Temp Sensor state for trigger expression.</p> | `0` |
| `{$TEMP.SENSOR.STATUS.CRIT:"overheatCritical"}` | <p>The critical value of the Temp Sensor state for trigger expression.</p> | `4` |
| `{$TEMP.SENSOR.STATUS.OK}` | <p>The OK status of the Temp Sensor for trigger expression.</p> | `1` |

## Template Items

### Static Items

| Name | Description | Type | Key | Additional Info |
|------|-------------|------|-----|-----------------|
| DataDomain: DDBoost Backup Connections | DATA-DOMAIN-MIB::ddboostStatsBackupConn<br>Number of Backup connections. | SNMP agent | dell.dd.boost.backup.con[ddboostStatsBackupConn] | Units: none<br>Tag: component=charts |
| DataDomain: DDBoost Restore Connections | DATA-DOMAIN-MIB::ddboostStatsRestoreConn<br>Number of Restore connections. | SNMP agent | dell.dd.boost.restore.con[ddboostStatsRestoreConn] | Units: none<br>Tag: component=charts |
| DataDomain: File System Status Message | DATA-DOMAIN-MIB::fileSystemStatusMessage | SNMP agent | dell.dd.fs.status.message | Value type: Text<br>Discard unchanged (1d)<br>Tag: component=filesystem |
| DataDomain: File System Status | DATA-DOMAIN-MIB::fileSystemStatus | SNMP agent | dell.dd.fs.status[fileSystemStatus] | Valuemap: DATA-DOMAIN-MIB::fileSystemStatus<br>Discard unchanged (1d)<br>Tag: component=filesystem |
| DataDomain: CIFS operations rate | DATA-DOMAIN-MIB::cifsOpsPerSecond<br>Number of CIFS Operations performed per second. | SNMP agent | dell.dd.sys.cifs.ops[cifsOpsPerSecond] | Units: ops<br>Tag: component=charts |
| DataDomain: Cpu Average Busy | DATA-DOMAIN-MIB::cpuAvgPercentageBusy<br>CPU average percentage busy. | SNMP agent | dell.dd.sys.cpu.avg.busy[cpuAvgPercentageBusy] | Units: %<br>Tag: component=charts |
| DataDomain: Cpu Max Busy | DATA-DOMAIN-MIB::cpuMaxPercentageBusy<br>CPU max percentage busy. | SNMP agent | dell.dd.sys.cpu.max.busy[cpuMaxPercentageBusy] | Units: %<br>Tag: component=charts |
| DataDomain: Disk Busy rate | DATA-DOMAIN-MIB::diskBusyPercentage<br>Percentage of Time Disks were busy. | SNMP agent | dell.dd.sys.disk.busy[diskBusyPercentage] | Units: %<br>Tag: component=charts |
| DataDomain: Disk Read rate | DATA-DOMAIN-MIB::diskReadKBytesPerSecond<br>Number of KBytes per second read from disk. | SNMP agent | dell.dd.sys.disk.read[diskReadKBytesPerSecond] | Units: B/s<br>Multiplier: ×1024<br>Tag: component=charts |
| DataDomain: Disk Write rate | DATA-DOMAIN-MIB::diskWriteKBytesPerSecond<br>Number of KBytes per second written to disk. | SNMP agent | dell.dd.sys.disk.write[diskWriteKBytesPerSecond] | Units: B/s<br>Multiplier: ×1024<br>Tag: component=charts |
| DataDomain: Hardware Model | DATA-DOMAIN-MIB::systemModelNumber<br>Model Number of the System | SNMP agent | dell.dd.sys.model[systemModelNumber] | Value type: Char<br>Inventory: MODEL<br>Discard unchanged (1d)<br>Tag: component=system |
| DataDomain: NFS operations rate | DATA-DOMAIN-MIB::nfsOpsPerSecond<br>Number of NFS Operations performed per second. | SNMP agent | dell.dd.sys.nfs.ops[nfsOpsPerSecond] | Units: ops<br>Tag: component=charts |
| DataDomain: System Notes | DATA-DOMAIN-MIB::sysNotes<br>Customer defined notes associated with this DD System | SNMP agent | dell.dd.sys.notes[sysNotes] | Update: 1h<br>Value type: Text<br>Inventory: NOTES<br>Discard unchanged (1d)<br>Tag: component=system |
| DataDomain: Serial Number | DATA-DOMAIN-MIB::systemSerialNumber<br>Serial Number of the System | SNMP agent | dell.dd.sys.serialnumber[systemSerialNumber] | Value type: Char<br>Inventory: SERIALNO_A<br>Discard unchanged (1d)<br>Tag: component=system |
| DataDomain: System Current Time | DATA-DOMAIN-MIB::systemCurrentTime<br>DDR system's current time | SNMP agent | dell.dd.sys.time[systemCurrentTime] | Value type: Char<br>Discard unchanged (1d)<br>Tag: component=system |
| DataDomain: System Version | DATA-DOMAIN-MIB::systemVersion<br>DD version of the system | SNMP agent | dell.dd.sys.version[systemVersion] | Update: 1h<br>Value type: Char<br>Inventory: OS<br>Discard unchanged (1d)<br>Tag: component=system |
| DataDomain: Uptime (hardware) | HOST-RESOURCES-MIB<br>Time since last hardware initialization | SNMP agent | dell.dd.system.hw.uptime[hrSystemUptime.0] | Units: uptime<br>Update: 30s<br>Multiplier: ×0.01<br>Tag: component=system |
| DataDomain: Uptime (network) | SNMPv2-MIB<br>Time since network management portion was re-initialized | SNMP agent | dell.dd.system.net.uptime[sysUpTime.0] | Units: uptime<br>Update: 30s<br>Multiplier: ×0.01<br>Tag: component=system |
| DataDomain: SNMP traps (fallback) | Item is used to collect all SNMP traps unmatched by other snmptrap items | SNMP trap | snmptrap.fallback | Value type: Log<br>Tag: Application=General |
| DataDomain: System contact details | SNMPv2-MIB::sysContact<br>Contact person information | SNMP agent | system.contact[sysContact.0] | Update: 1h<br>Inventory: CONTACT<br>Discard unchanged (1d)<br>Tag: Application=General |
| DataDomain: System location | SNMPv2-MIB::sysLocation<br>Physical location | SNMP agent | system.location[sysLocation.0] | Update: 1h<br>Inventory: LOCATION<br>Discard unchanged (1h)<br>Tag: Application=General |
| DataDomain: System name | SNMPv2-MIB::sysName<br>Administratively-assigned name (usually FQDN) | SNMP agent | system.name | Update: 1h<br>Inventory: NAME<br>Discard unchanged (1h)<br>Tag: Application=General |
| DataDomain: System object ID | SNMPv2-MIB::sysObjectID<br>Vendor's authoritative identification | SNMP agent | system.objectid[sysObjectID.0] | Update: 15m<br>Discard unchanged (1h)<br>Tag: Application=General |
| DataDomain: SNMP agent availability | Internal item checking SNMP availability | Internal | zabbix[host,snmp,available] | Tag: Application=Status |

## Template Triggers (Static Items)

| Name | Description | Expression | Severity | Dependencies | Additional Info |
|------|-------------|------------|----------|--------------|-----------------|
| File System Status is not in optimal state | Check File System | last(/DELL PowerProtect DataDomain SNMP/dell.dd.fs.status[fileSystemStatus])<>3 | Warning | None | Manual close: YES<br>Tag: scope=availability |
| DataDomain: Device has been replaced | Device serial number has changed. Ack to close | last(...serialnumber,#1)<>last(...serialnumber,#2) and length(last(...serialnumber))>0 | Information | None | Manual close: YES<br>Tag: scope=notice |
| DataDomain: System Version has changed | System version has changed. Ack to close. | last(...systemVersion,#1)<>last(...systemVersion,#2) and length(last(...systemVersion))>0 | Information | None | Manual close: YES<br>Tag: scope=notice |
| DataDomain: System name has changed | The name of the system has changed. Acknowledge to close the problem manually. | last(/.../system.name,#1)<>last(/.../system.name,#2) and length(last(...system.name))>0 | Information | None | Manual close: YES<br>Tags: scope=notice, security |
| DataDomain: No SNMP data collection | SNMP is not available for polling. Please check device connectivity and SNMP settings. | max(/.../zabbix[host,snmp,available],{$SNMP.TIMEOUT})=0 | Warning | None | Tag: scope=availability |
| DataDomain: Host has been restarted | Uptime is less than 10 minutes. | (last(hw.uptime)>0 and last(hw.uptime)<10m) or (last(hw.uptime)=0 and last(net.uptime)<10m) | Warning | None | Manual close: YES<br>Tag: scope=notice |

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
