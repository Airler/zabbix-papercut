# Zabbix template for PaperCut NG and PaperCut MF monitoring

## Overview

The template to monitor PaperCut MF and PaperCut NG by Zabbix 6.x using HTTP agent.

## Setup

> See [Zabbix templates importing](https://www.zabbix.com/documentation/5.2/manual/xml_export_import/templates#importing) for basic instructions on how to import a template.

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
|{$PAPERCUT_AUTH_KEY} |<p>PaperCut authentication key. (http://localhost:9191/app?service=page/OptionsAdvanced)</p> |`` |
|{$PAPERCUT_PORT} |<p>Port on which PaperCut is listening.</p> |`` |
|{$PAPERCUT.NODATA_TIMEOUT} |<p>Timeout after which no data trigger will be executed.</p> |``30m |

## Template links

There are no template links in this template.

## Discovery rules

|Name|Description|Type|Key and additional info|
|----|-----------|----|----|
TODO

## Items collected

|Name|Description|
|----------|--------------|
TODO

## Triggers

Appropriate triggers are associated with the items

## Feedback

Please report any issues with the template here in the "Issues" tab.
