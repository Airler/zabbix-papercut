# Zabbix template for PaperCut NG and MF monitoring

## Overview

The template to monitor PaperCut MF and PaperCut NG by Zabbix 6.x using HTTP agent.

## Setup

> See [Zabbix templates importing](https://www.zabbix.com/documentation/5.2/manual/xml_export_import/templates#importing) for basic instructions on how to import a template.

Create a PaperCut host and link this template to it.

## Zabbix configuration

- Set/change the {$PAPERCUT_AUTH_KEY} macro in host settings to match your authorization key. See [Get PaperCut Monitoring details](https://www.papercut.com/kb/Main/SystemHealthZabbix#step-1-get-the-papercut-ng-or-mf-system-health-monitoring-details)
- Set/change the {$PAPERCUT_PORT} macro in host settings to match your PaperCut port.

## Template links

This template does not require additional templates.

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
