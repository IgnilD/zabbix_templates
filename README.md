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

## Discovery Rules

The template uses Low-Level Discovery (LLD) to automatically create items and triggers for dynamic components.

| Discovery Rule Name                  | Description                                                                 | Update Interval | Status    | Discovered Macros / LLD Macros                  | Notes |
|--------------------------------------|-----------------------------------------------------------------------------|-----------------|-----------|--------------------------------------------------|-------|
| DDBoost Connections discovery        | Discovers DDBoost interfaces (DATA-DOMAIN-MIB::ddboostInterface)            | 1h              | Disabled  | `{#INTERFAC}`                                    | Disabled by default – enable if needed |
| Disk discovery                       | Discovers disks with enclosure ID and index                                 | 1h              | Enabled   | `{#DISK_ENCLOSUREID}`, `{#DISK_INDEX}`           | Creates items for capacity, model, serial, firmware, state |
| Enclosure Discovery                  | Discovers storage enclosures                                                | 1h              | Enabled   | `{#ENCLOSURE_NR}`                                | Creates items for model, serial, capacity |
| FAN discovery                        | Discovers fans per enclosure                                                | 1h              | Enabled   | `{#FAN_ENCLOSUREID}`, `{#FAN_DESCR}`             | Creates items for speed level and status |
| FS discovery                         | Discovers file system resources (name + tier)                               | 1h              | Enabled   | `{#FS_INDEX}`, `{#FS_NAME}`, `{#FS_TIER}`         | Creates space used/available/cleanable items and utilization triggers |
| Network interfaces discovery         | Standard IF-MIB interface discovery with advanced filtering                 | 1h              | Enabled   | `{#IFNAME}`, `{#IFALIAS}`, `{#IFDESCR}`, `{#IFOPERSTATUS}`, `{#IFADMINSTATUS}`, `{#IFTYPE}` | Extensive traffic, error, speed, status items + triggers |
| NVRAM BBU Discovery                  | Discovers NVRAM backup battery units                                        | 1h              | Enabled   | `{#BBU_INDEX}`                                   | Creates charge % and status items |
| NVRAM Discovery                      | Discovers NVRAM cards                                                       | 1h              | Enabled   | `{#NVRAM_INDEX}`                                 | Creates memory size and error count items |
| Ports Discovery                      | Discovers physical ports (only those reporting speed in bps)                 | 1h              | Enabled   | `{#PORT}`, `{#PORT_TYPE}`, `{#PORT_LINK}`         | Monitors link speed changes |
| PSU Discovery                        | Discovers power supply units per enclosure                                  | 1h              | Enabled   | `{#PSU_ENCLOSUREID}`, `{#PSU_DESCR}`             | Creates status items |
| Temperature discovery                | Discovers temperature sensors per enclosure                                 | 10m             | Enabled   | `{#TEMP_ENCLOSUREID}`, `{#TEMP_DESCR}`           | Creates temperature value (°C) and status items |

### Discovered Item Prototypes (Summary)

| Component          | Created Items                                                                                              | Additional Info |
|--------------------|------------------------------------------------------------------------------------------------------------|-----------------|
| **DDBoost**        | Backup connections, Restore connections, Total connections per interface                                   | Tag: component=charts |
| **Disks**          | Capacity, Firmware version, Model, Serial number, State (with valuemap)                                     | Discard unchanged (6h) |
| **Enclosures**     | Capacity, Model, Serial number                                                                             | Update: daily/weekly |
| **Fans**           | Speed level (valuemap), Status (valuemap)                                                                  | Discard unchanged (6h) |
| **File Systems**   | Space available, cleanable, size, used (B), used (%)                                                       | Multiplier ×1,073,741,824 for GB→B |
| **Network**        | Inbound/outbound bits (bps), packets with errors/discards, speed, operational status, interface type       | Change per second, multipliers where needed |
| **NVRAM BBU**      | Battery charge (%), Status (valuemap)                                                                      | Discard unchanged (6h) |
| **NVRAM**          | Total memory (B), Memory error count, PCI error count                                                      | Discard unchanged (6h) |
| **Ports**          | Link speed (text)                                                                                          | Discard unchanged (6h) |
| **PSU**            | Status (valuemap)                                                                                          | Discard unchanged (6h) |
| **Temperature**    | Current value (°C), Status (valuemap)                                                                      | Discard unchanged (6h) |

### Discovered Trigger Prototypes (Summary)

| Component          | Trigger Name                                                                 | Severity   | Description / Notes |
|--------------------|------------------------------------------------------------------------------|------------|---------------------|
| **Disks**          | Disk {#DISK_INDEX} of Enclosure {#DISK_ENCLOSUREID} is in critical state      | Average    | absent / failed / unknown |
| **Disks**          | Disk {#DISK_INDEX} of Enclosure {#DISK_ENCLOSUREID} make reconstruction       | Information| copyReconstruction / raidReconstruction |
| **Fans**           | {#FAN_DESCR} of Enclosure {#FAN_ENCLOSUREID} is in critical state             | Average    | fail / notfound |
| **File Systems**   | {#FS_NAME} of {#FS_TIER} Tier space is low                                   | Warning    | > {$FS.SPACE.WARN}% (depends on critical) |
| **File Systems**   | {#FS_NAME} of {#FS_TIER} Tier space is too low                                | High       | > {$FS.SPACE.CRIT}% |
| **Network**        | Interface {#IFNAME}({#IFALIAS}): Link down                                    | Average    | With recovery expression, manual close |
| **Network**        | Interface {#IFNAME}({#IFALIAS}): Ethernet has changed to lower speed         | Information| Speed drop detection |
| **Network**        | Interface {#IFNAME}({#IFALIAS}): High bandwidth usage                         | Warning    | Utilisation > {$IF.UTIL.MAX} % |
| **Network**        | Interface {#IFNAME}({#IFALIAS}): High error rate                              | Warning    | Errors > {$IF.ERRORS.WARN} threshold |
| **NVRAM BBU**      | Battery Unit {#BBU_INDEX} have low charge                                    | Warning    | < {$NVRAM.BATTERY.CHARGE.WARN} |
| **NVRAM BBU**      | Battery Unit {#BBU_INDEX} is in critical state                               | Average    | Discharged status |
| **NVRAM BBU**      | Battery Unit {#BBU_INDEX} is in warning state                                 | Warning    | Disabled / softdisabled |
| **NVRAM BBU**      | Battery Unit {#BBU_INDEX} is not in optimal state                            | Warning    | Any non-OK state (depends on above) |
| **NVRAM**          | Memory Error on NVRAM {#NVRAM_INDEX}                                          | Average    | Count ≠ 0 |
| **NVRAM**          | PCI Error on NVRAM {#NVRAM_INDEX}                                             | Average    | Count ≠ 0 |
| **Ports**          | {#PORT} ({#PORT_TYPE}) Link Speed changed                                    | Average    | Speed change or empty value |
| **PSU**            | {#PSU_DESCR} of Enclosure {#PSU_ENCLOSUREID} is in critical state            | Average    | acnone / failed / faulty |
| **PSU**            | {#PSU_DESCR} of Enclosure {#PSU_ENCLOSUREID} is in warning state             | Warning    | absent / unknown |
| **Temperature**    | "{#TEMP_DESCR}" of Enclosure {#TEMP_ENCLOSUREID} is in critical status        | Average    | overheatCritical / failed |
| **Temperature**    | "{#TEMP_DESCR}" of Enclosure {#TEMP_ENCLOSUREID} is not in optimal status    | Warning    | Any non-OK state (depends on critical) |

All discovered triggers support manual close where appropriate and use relevant tags (availability, performance, etc.).
