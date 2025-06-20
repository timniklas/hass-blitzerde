# Blitzer.de Integration for Home Assistant 🏠

[![GitHub Release](https://img.shields.io/github/v/release/timniklas/hass-blitzerde?sort=semver&style=for-the-badge&color=green)](https://github.com/timniklas/hass-blitzerde/releases/)
[![GitHub Release Date](https://img.shields.io/github/release-date/timniklas/hass-blitzerde?style=for-the-badge&color=green)](https://github.com/timniklas/hass-blitzerde/releases/)
![GitHub Downloads (all assets, latest release)](https://img.shields.io/github/downloads/timniklas/hass-blitzerde/latest/total?style=for-the-badge&label=Downloads%20latest%20Release)
![HA Analytics](https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fanalytics.home-assistant.io%2Fcustom_integrations.json&query=%24.blitzerde.total&style=for-the-badge&label=Active%20Installations&color=red)
![GitHub commit activity](https://img.shields.io/github/commit-activity/m/timniklas/hass-blitzerde?style=for-the-badge)
[![hacs](https://img.shields.io/badge/HACS-Integration-blue.svg?style=for-the-badge)](https://github.com/hacs/integration)

## Overview

The Blitzer.de Home Assistant Custom Integration allows you to integrate the Blitzer.de App with your Home Assistant setup.

## Example Markdown Card

### Code

```
<h1><img src="/local/Blitzer_app.svg"  height="23"> Achtung!</h1>
{%- set sensor_names = ["YOUR_SENSOR_NAME"] %}
{%- for city in sensor_names %}
{%- set anzahl_aktuelle_warnungen = states("sensor.blitzerde_blitzerde_"~city~"_total") | int(0) %}
{%- if anzahl_aktuelle_warnungen > 0 %}
{%- set blitzer_name = state_attr("binary_sensor.blitzerde_blitzerde_"~city~"_map1", "friendly_name")[0:-1] %}
<b>{{blitzer_name}} ({{anzahl_aktuelle_warnungen}})</b><br>
{%- for i in range(int(anzahl_aktuelle_warnungen)) %}
{%- set blitzer_backend = state_attr("binary_sensor.blitzerde_blitzerde_"~city~"_map"~ loop.index, "backend") %}
{%- set blitzer_vmax = state_attr("binary_sensor.blitzerde_blitzerde_"~city~"_map"~ loop.index, "vmax") %}
{%- set blitzer_street = state_attr("binary_sensor.blitzerde_blitzerde_"~city~"_map"~ loop.index, "street") %}
{%- set blitzer_counter = state_attr("binary_sensor.blitzerde_blitzerde_"~city~"_map"~ loop.index, "counter") %}
{%- set blitzer_image = state_attr("binary_sensor.blitzerde_blitzerde_"~city~"_map"~ loop.index, "entity_picture") %}
<img src="{{blitzer_image}}" width="20">
<a href="https://map.blitzer.de/v5/ID/{{blitzer_backend}}/">{{blitzer_street}}</a> bei {{blitzer_vmax}} km/h&nbsp;&nbsp;
{%- for i in range(int(blitzer_counter)) %}
<img src="https://map.blitzer.de/v5/images/star_full.svg" width="12">
{%- endfor %}
{%- for i in range(3-int(blitzer_counter)) %}
<img src="https://map.blitzer.de/v5/images/star_contour.svg" width="12">
{%- endfor %}
<br>
{%- endfor %}
{%- if not loop.last %}<br>{%- endif %}
{%- endif %}
{%- endfor %}
```

### Screenshot
![image](https://github.com/user-attachments/assets/2c230648-423b-427a-a9bf-b5c129883262)

![image](https://github.com/user-attachments/assets/ab470939-f692-4b7e-9dc1-ce73cd5b2371)


## Installation

### HACS (recommended)

This integration is available in HACS (Home Assistant Community Store).

1. Install HACS if you don't have it already
2. Open HACS in Home Assistant
3. Go to any of the sections (integrations, frontend, automation).
4. Click on the 3 dots in the top right corner.
5. Select "Custom repositories"
6. Add following URL to the repository `https://github.com/timniklas/hass-blitzerde`.
7. Select Integration as category.
8. Click the "ADD" button
9. Search for "Blitzer.de"
10. Click the "Download" button

### Manual

To install this integration manually you have to download [_blitzerde.zip_](https://github.com/timniklas/hass-blitzerde/releases/latest/) and extract its contents to `config/custom_components/blitzerde` directory:

```bash
mkdir -p custom_components/blitzerde
cd custom_components/blitzerde
wget https://github.com/timniklas/hass-blitzerde/releases/latest/download/blitzerde.zip
unzip blitzerde.zip
rm blitzerde.zip
```

## Configuration

### Using UI

[![Open your Home Assistant instance and start setting up a new integration.](https://my.home-assistant.io/badges/config_flow_start.svg)](https://my.home-assistant.io/redirect/config_flow_start/?domain=blitzerde)

From the Home Assistant front page go to `Configuration` and then select `Devices & Services` from the list.
Use the `Add Integration` button in the bottom right to add a new integration called `Blitzer.de`.

## Help and Contribution

If you find a problem, feel free to report it and I will do my best to help you.
If you have something to contribute, your help is greatly appreciated!
If you want to add a new feature, add a pull request first so we can discuss the details.

## Disclaimer

This custom integration is not officially endorsed or supported by Blitzer.de.
Use it at your own risk and ensure that you comply with all relevant terms of service and privacy policies.
