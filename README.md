# Liquid Level Detection System

This repository contains a custom liquid level monitoring system that my dad and I built for our gas station’s car wash. The system was originally designed to monitor car wash soap levels, but the same setup can be adapted for other liquids and containers as well.

It uses a VL53L1X time-of-flight distance sensor and an ESP8266-based microcontroller to measure the level inside a container. The sensor reads the distance from the top of the container down to a floating target/bobber. As the liquid level changes, the measured distance changes.

The sensor data is sent over MQTT and read by Home Assistant, where it can be displayed as distance, percentage, or estimated volume remaining.

## Why We Built This

At the gas station, the car wash depends on liquid chemical containers that need to be checked regularly. Before this system, checking levels was a manual process. Someone had to physically inspect the containers, which was easy to forget during a busy day.

This project was built to make that process smarter. Instead of constantly checking containers by hand, the system lets us monitor liquid levels through Home Assistant. That makes it easier to know when a container is getting low before it becomes a problem.

## How It Works

The system is mounted on top of the container. A VL53L1X distance sensor points downward and measures the distance to a floating target inside the container. As the liquid level drops, the distance reading increases. As the liquid level rises, the distance reading decreases.

The ESP8266 reads the sensor data, converts it into useful values, and publishes those values over MQTT. Home Assistant then uses a YAML MQTT sensor configuration to create readable entities for a dashboard.

The Home Assistant YAML can display values such as:

- Raw distance in millimeters
- Distance in centimeters
- Distance in inches
- Liquid level percentage
- Estimated gallons remaining

These values allow the container to be monitored from a Home Assistant dashboard instead of needing to physically check the container every time.

## Home Assistant and MQTT

Home Assistant and MQTT are the software/integration side of this project.

The ESP8266 publishes sensor readings to MQTT topics. Home Assistant subscribes to those topics using the YAML configuration included in this repository. This creates sensor entities that can be used in dashboards, automations, notifications, and alerts.

For example, Home Assistant can be used to send a notification when a liquid container drops below a certain percentage. This helps prevent unexpected runouts and keeps the system easier to manage.

## Hardware Used

- ESP8266 ESP-12 / ESP-12F microcontroller board
- Adafruit VL53L1X Time of Flight distance sensor
- I2C Qwiic / STEMMA QT 4-pin cable kit
- 20mm 2006 12V blower fan
- Micro USB splitter cable
- M2 male/female brass hex spacer standoffs
- M2 heat-set threaded inserts
- 3D printed sensor cap / enclosure
- Floating target / bobber for the sensor to read
- Wiring, fasteners, and basic mounting hardware

## Software / Integrations

- Arduino IDE
- ESP8266 Arduino board package
- MQTT
- Home Assistant
- Home Assistant MQTT sensor YAML
- OTA update support

## Physical Setup Notes

The sensor is mounted at the top of the container and aimed downward. A floating target is used inside the container so the sensor has a consistent surface to read from.

The cap/enclosure was 3D printed and modified for the sensor, wiring, and mounting hardware. We also drilled small holes into each tube to avoid pressure buildup inside the container, since pressure changes could affect the floating target and create incorrect readings.

The annotated project photos show the internal sensor mount, wiring layout, 3D printed cap, bobber/target setup, drilled vent holes, and the installed containers at the car wash.

## Code and Development

Most of the code and YAML was generated with help from ChatGPT. My dad operates the gas station, and I am a full-time student, so using AI helped us move faster and turn the idea into a working system without having to write every piece from scratch.

I still reviewed, tested, adjusted, and applied the code to the real hardware setup. The project was built through trial, testing, and real-world installation at the car wash.

## Repository Contents

This repository includes:

- ESP8266 Arduino code for the VL53L1X sensor
- Home Assistant MQTT YAML sensor configuration
- Setup documentation
- Annotated photos of the physical build
- Parts list / BOM for the hardware
- Notes for wiring, installation, calibration, and testing

## Current Status

The system is designed as a practical monitoring tool for our car wash. It is not a commercial product, but it is a working custom-built solution for our specific setup.

Future improvements could include:

- Adding support for more containers
- Creating Home Assistant alerts for low liquid levels
- Improving calibration
- Building a cleaner Home Assistant dashboard
- Adding long-term usage tracking
- Improving the enclosure for daily shop use
- Making the setup easier to reproduce for other liquids or container sizes

## Project Goal

The main goal of this project is simple: make it easier to monitor liquid levels without constantly checking containers by hand.

By combining a distance sensor, microcontroller, MQTT, and Home Assistant, we turned a manual maintenance task into something that can be monitored automatically.
