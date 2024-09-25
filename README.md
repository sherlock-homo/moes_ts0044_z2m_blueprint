# Moes 4-Button Scene Switch Z2M (TS0044) Blueprint
### Easily Automate TS0044 Devices Paired via Zigbee2MQTT (Z2M)
#
[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fcommunity.home-assistant.io%2Ft%2Fmoes-4-button-scene-controller-zigbee2mqtt-model-ts0044%2F774469)
![Moes TS0044 Scene Switch with Box|250x170](https://github.com/sherlock-homo/moes_ts0044_z2m_blueprint/blob/main/moes_ts0044_box.png) ![Zigbee2MQTT Logo|175x175](https://github.com/sherlock-homo/moes_ts0044_z2m_blueprint/blob/main/z2m_logo.png)

## Description
This blueprint is designed for the Moes 4-Button Scene Switch (TS0044), integrated with Zigbee2MQTT. It condenses all 12 unique button actions for a Scene Switch into a single, easy-to-maintain automation. It supports the following actions for each button:

- **Single Press** -- single_press
- **Double Press** -- double_press
- **Hold** -- hold_press

This blueprint allows you to quickly and easily configure multiple actions for each button on the scene switch, making it a versatile tool for managing your smart home devices.

## Prerequisites

Ensure your device is properly integrated with Zigbee2MQTT. You'll need to locate the MQTT topic associated with your scene switch before setting up the blueprint.

#### *Note*: 
* To expose the actions in Z2M for use in Home Assistant automations, I needed to manually select each button/action on the Scene Switch (e.g., single-click, double-click, and hold every button on the device following initial pairing with Z2M). Without this step, Home Assistant didn't seem to recognize the actions in the automation YAML. 

* If you run into this issue, try this out to see if the actions are exposed and registered in Home Assistant. If that doesn't work, try trailing the Z2M logs and monitor action payloads to that MQTT topic. Every payload reference for each value_template in the YAML below should match the actions exposed by your device.

#### Steps to find your device's MQTT topic:

1. Navigate to the Zigbee2MQTT integration in Home Assistant.
2. Select "Logs" from the ribbon header.
3. Press any button on your Moes Scene Switch.
4. Locate the latest log entry and note the MQTT topic displayed.

## Device Information:
![Moes TS0044 Scene Switch|250x250](https://github.com/sherlock-homo/moes_ts0044_z2m_blueprint/blob/main/moes_ts0044_switch.png)

- **Manufacturer**: Moes (Tuya)
- **Device Type**: 4-Button Scene Switch
- **Model**: TS0044
- **Zigbee Manufacturer**: _TZ3000_wkai4ga5
- **Zigbee2MQTT Device Info**: [Link to TS0044](https://www.zigbee2mqtt.io/devices/TS0044.html)
- **Switch Button Action Correlations**:
    1. Top-Left
    2. Top-Right
    3. Bottom-Left
    4. Bottom-Right

## How to Use

1. **Import the Blueprint**: [Click to Import Blueprint](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fcommunity.home-assistant.io%2Ft%2Fmoes-4-button-scene-controller-zigbee2mqtt-model-ts0044%2F774469) or select the "Import Blueprint" button at the top of this post.
2. **Configure**: Use the MQTT topic you found earlier in the "switch_topic" field. Assign actions to each button press (single, double, or hold) using the blueprint inputs.
3. **Test**: Save and test your automation. If you run into any issues, feel free to leave a comment below.


## Blueprint YAML

```yaml
blueprint:
  name: Moes/Tuya 4-Button Scene Switch (TS0044)
  description: >
    Controls various entities based on single and double press actions from a Moes 4-Button Scene Switch.
  domain: automation
  input:
    switch_topic:
      name: MQTT Topic
      description: The MQTT topic for the scene switch.
      selector:
        text:
    single_1:
      name: Action for 1 Single Press
      description: Action to run when button 1 is single pressed.
      selector:
        action: {}
    single_2:
      name: Action for 2 Single Press
      description: Action to run when button 2 is single pressed.
      selector:
        action: {}
    single_3:
      name: Action for 3 Single Press
      description: Action to run when button 3 is single pressed.
      selector:
        action: {}
    single_4:
      name: Action for 4 Single Press
      description: Action to run when button 4 is single pressed.
      selector:
        action: {}
    double_1:
      name: Action for 1 Double Press
      description: Action to run when button 1 is double pressed.
      selector:
        action: {}
    double_2:
      name: Action for 2 Double Press
      description: Action to run when button 2 is double pressed.
      selector:
        action: {}
    double_3:
      name: Action for 3 Double Press
      description: Action to run when button 3 is double pressed.
      selector:
        action: {}
    double_4:
      name: Action for 4 Double Press
      description: Action to run when button 4 is double pressed.
      selector:
        action: {}
    hold_1:
      name: Action for 1 hold Press
      description: Action to run when button 1 is held.
      selector:
        action: {}
    hold_2:
      name: Action for 2 hold Press
      description: Action to run when button 2 is held.
      selector:
        action: {}
    hold_3:
      name: Action for 3 hold Press
      description: Action to run when button 3 is held.
      selector:
        action: {}
    hold_4:
      name: Action for 4 hold Press
      description: Action to run when button 4 is held.
      selector:
        action: {}

trigger:
  - platform: mqtt
    topic: !input switch_topic

action:
  - choose:
      - conditions:
          - condition: template
            value_template: "{{ trigger.payload == '1_single' }}"
        sequence: !input single_1

      - conditions:
          - condition: template
            value_template: "{{ trigger.payload == '2_single' }}"
        sequence: !input single_2

      - conditions:
          - condition: template
            value_template: "{{ trigger.payload == '3_single' }}"
        sequence: !input single_3

      - conditions:
          - condition: template
            value_template: "{{ trigger.payload == '4_single' }}"
        sequence: !input single_4

      - conditions:
          - condition: template
            value_template: "{{ trigger.payload == '1_double' }}"
        sequence: !input double_1

      - conditions:
          - condition: template
            value_template: "{{ trigger.payload == '2_double' }}"
        sequence: !input double_2

      - conditions:
          - condition: template
            value_template: "{{ trigger.payload == '3_double' }}"
        sequence: !input double_3

      - conditions:
          - condition: template
            value_template: "{{ trigger.payload == '4_double' }}"
        sequence: !input double_4
		
      - conditions:
          - condition: template
            value_template: "{{ trigger.payload == '1_hold' }}"
        sequence: !input hold_1

      - conditions:
          - condition: template
            value_template: "{{ trigger.payload == '2_hold' }}"
        sequence: !input hold_2

      - conditions:
          - condition: template
            value_template: "{{ trigger.payload == '3_hold' }}"
        sequence: !input hold_3

      - conditions:
          - condition: template
            value_template: "{{ trigger.payload == '4_hold' }}"
        sequence: !input hold_4

mode: single
```
