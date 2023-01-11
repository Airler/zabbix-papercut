# Zabbix template for PaperCut NG and PaperCut MF monitoring

## Overview

The template to monitor PaperCut MF and PaperCut NG by Zabbix 6.x using HTTP agent.

## Setup

> See [Zabbix templates importing](https://www.zabbix.com/documentation/6.0/manual/xml_export_import/templates#importing) for basic instructions on how to import a template.

1. Create a new host
2. Set/change the host macros required for PaperCut authentication:
```text
{$PAPERCUT_AUTH_KEY}
{$PAPERCUT_PORT}
```
3. Link the template to host created early

## Zabbix configuration

No specific Zabbix configuration is required

### Macros used

|Name|Description|Default|
|----|-----------|-------|
|{$PAPERCUT_AUTH_KEY} |<p>PaperCut authentication key. (see http://localhost:9191/app?service=page/OptionsAdvanced on PaperCut server)</p> | |
|{$PAPERCUT_PORT} |<p>Port on which PaperCut is listening.</p> |`9191` |
|{$PAPERCUT.NODATA_TIMEOUT} |<p>Timeout after which no data trigger will be executed.</p> |`30m` |

## Template links

There are no template links in this template.

## Discovery rules

|Name|Description|Type|Key and additional info|
|----|-----------|----|----|
|PaperCut device discovery|Discovery of all printer devices from PaperCut|DEPENDENT|papercut.device.discovery <p>**Preprocessing**:<br>- JSONPath: `$.devices`<br>- DISCARD_UNCHANGED_HEARTBEAT: `6h`</p> |
|PaperCut printer discovery|Discovery of all printers from PaperCut|DEPENDENT|papercut.printer.discovery <p>**Preprocessing**:<br>- JSONPath: `$.printers`<br>- DISCARD_UNCHANGED_HEARTBEAT: `6h`</p> |

## Items collected

|Name|Description|Type|Key and additional info|
|----------|--------------|----------|----------|
|PaperCut API: Devices| |HTTP_Agent|papercut.api.devices|
|PaperCut API: Monitoring| |HTTP_Agent|papercut.api|
|PaperCut API: Printers| |HTTP_Agent|papercut.api.printers|
|PaperCut Database Active Connections| |DEPENDENT|papercut.database.activeConnections <p>**Preprocessing**:<br>- JSONPath: `$.database.activeConnections`</p> |
|PaperCut Database Max Connections| |DEPENDENT|papercut.database.maxConnections <p>**Preprocessing**:<br>- JSONPath: `$.database.maxConnections`</p> |
|PaperCut Database Status| |DEPENDENT|papercut.database.status <p>**Preprocessing**:<br>- JSONPath: `$.database.status`</p> |
|PaperCut Devices Count| |DEPENDENT|papercut.devices.total <p>**Preprocessing**:<br>- JSONPath: `$.devices.count`</p> |
|PaperCut Devices in Error| |DEPENDENT|papercut.devices.inErrorCount <p>**Preprocessing**:<br>- JSONPath: `$.devices.inErrorCount`</p> |
|PaperCut Devices in Error Percentage| |DEPENDENT|papercut.devices.inErrorPercentage <p>**Preprocessing**:<br>- JSONPath: `$.devices.inErrorPercentage`</p> |
|PaperCut Disk Space Free| |DEPENDENT|papercut.system.diskspace.free <p>**Preprocessing**:<br>- JSONPath: `$.applicationServer.systemMetrics.diskSpaceFreeMB`<br>- Custom multiplier: `1024000`</p> |
|PaperCut DiskSpace Used| |DEPENDENT|papercut.system.diskspace.used <p>**Preprocessing**:<br>- JSONPath: `$.applicationServer.systemMetrics.diskSpaceUsedPercentage`</p> |
|PaperCut Held Jobs Count| |DEPENDENT|papercut.printers.heldJobCountTotal <p>**Preprocessing**:<br>- JSONPath: `$.printers.heldJobCountTotal`</p> |
|PaperCut Held Jobs Count Max| |DEPENDENT|papercut.printers.heldJobsCountMax <p>**Preprocessing**:<br>- JSONPath: `$.printers.heldJobsCountMax`</p> |
|PaperCut JVM Memory Used Percentage| |DEPENDENT|papercut.system.jvmMemoryUsed <p>**Preprocessing**:<br>- JSONPath: `$.applicationServer.systemMetrics.jvmMemoryUsedPercentage`</p> |
|PaperCut printed pages in the last 60 minutes| |HTTP_Agent|papercut.api.stats.recentPagesCount <p>**Preprocessing**:<br>- JSONPath: `$.recentPagesCount`</p> |
|PaperCut Printers Count| |DEPENDENT|papercut.printers.total <p>**Preprocessing**:<br>- JSONPath: `$.printers.count`</p> |
|PaperCut Printers in Error| |DEPENDENT|papercut.printers.inErrorCount <p>**Preprocessing**:<br>- JSONPath: `$.printers.inErrorCount`</p> |
|PaperCut Printers in Error Percentage| |DEPENDENT|papercut.printers.inErrorPercentage <p>**Preprocessing**:<br>- JSONPath: `$.printers.inErrorPercentage`</p> |
|PaperCut Uptime| |DEPENDENT|papercut.system.uptimeHours <p>**Preprocessing**:<br>- JSONPath: `$.applicationServer.systemMetrics.uptimeHours`</p> |
|PaperCut Valid License| |DEPENDENT|papercut.license.valid <p>**Preprocessing**:<br>- JSONPath: `$.license.valid`</p> |
|PaperCut Valid License Remaining Days| |DEPENDENT|papercut.license.upgradeAssuranceRemainingDays <p>**Preprocessing**:<br>- JSONPath: `$.license.upgradeAssuranceRemainingDays`<br>- Custom multiplier: `86400`</p> |
|PaperCut Version| |DEPENDENT|papercut.system.version <p>**Preprocessing**:<br>- JSONPath: `$.applicationServer.systemInfo.version`</p> |
|Percentage Active Connections| |Calculated|papercut.database.activeConnections.percentage|
|Device {#DEVICE_NAME}: Status| |DEPENDENT|papercut.device.status["{#DEVICE_NAME}"] <p>**Preprocessing**:<br>- JSONPath: `$.devices[?(@.name == "{#DEVICE_NAME}")].state.status.first()`</p> |
|Device {#DEVICE_NAME}: Status Description| |DEPENDENT|papercut.device.status.description["{#DEVICE_NAME}"] <p>**Preprocessing**:<br>- JSONPath: `$.devices[?(@.name == "{#DEVICE_NAME}")].state.statusDescription.first()`</p> |
|Printer {#PRINTER_NAME}: Held Jobs| |DEPENDENT|papercut.printer.heldjobs["{#PRINTER_NAME}"] <p>**Preprocessing**:<br>- JSONPath: `$.printers[?(@.name == "{#PRINTER_NAME}")].heldJobsCount.first()`</p>|
|Printer {#PRINTER_NAME}: Status| |DEPENDENT|papercut.printer.status["{#PRINTER_NAME}"] <p>**Preprocessing**:<br>- JSONPath: `$.printers[?(@.name == "{#PRINTER_NAME}")].status.first()`</p>|

## Triggers

Appropriate triggers are associated with the items

## Feedback

Please report any issues with the template here in the "Issues" tab.
