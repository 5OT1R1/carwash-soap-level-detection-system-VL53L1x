# Car Wash Soap Detection System

This repository contains a custom soap level monitoring system that my dad and I built for our gas station’s car wash. The goal of the project is to reduce manual checking, prevent unexpected soap runouts, and make the car wash easier to monitor day-to-day.

The system uses a VL53L1X time-of-flight distance sensor with an ESP8266-based microcontroller to measure the soap level inside a container. The sensor reads the distance from the top of the container down to a floating target/bobber, then reports that value over MQTT. Home Assistant reads those MQTT topics and displays the soap level as distance, percentage, and estimated gallons.

## Why We Built This

At the gas station, the car wash depends on chemical containers that need to be checked regularly. Before this system, checking soap levels was a manual process. That meant someone had to physically inspect the containers, which was easy to forget during a busy day.

This project was built to make that process smarter. Instead of constantly checking the containers by hand, the system lets us monitor soap levels through Home Assistant. That makes it easier to know when soap is getting low before it becomes a problem.

## How It Works

The system is mounted on top of the soap container. A VL53L1X distance sensor points downward and measures the distance to a floating target inside the container. As the soap level drops, the distance reading changes.

The ESP8266 reads the sensor data, converts it into useful values, and publishes those values over MQTT. Home Assistant then uses a YAML MQTT sensor configuration to create readable entities for the dashboard.

The Home Assistant YAML includes sensors for:

- Raw distance in millimeters
- Distance in centimeters
- Distance in inches
- Soap percentage
- Estimated gallons remaining

These values allow the soap container to be monitored from a Home Assistant dashboard instead of needing to physically check the container every time.

## Home Assistant Integration

Home Assistant is a major part of this project. The microcontroller publishes MQTT data, and Home Assistant subscribes to those MQTT topics using the YAML configuration included in this repository.

The YAML file creates sensor entities such as `Soap1 Distance`, `Soap1 Percentage`, and `Soap1 Gallons`. These entities can then be added to dashboards, automations, notifications, or alerts.

For example, Home Assistant could be used to send a notification when the soap percentage drops below a certain level, helping prevent the car wash from running out unexpectedly.

## Hardware Used

- ESP8266 / NodeMCU-style microcontroller
- VL53L1X time-of-flight distance sensor
- 3D printed top cap / mounting piece
- Floating bobber or target inside the soap container
- Power supply
- MQTT broker
- Home Assistant

## Physical Setup Notes

The sensor is mounted at the top of the container and aimed downward. A floating target is used inside the container so the sensor has a consistent surface to read from. We also made adjustments to the container cap and tubing so pressure buildup or movement inside the container would not cause incorrect readings.

The annotated project photos show the internal sensor mount, wiring layout, 3D printed cap, bobber/target setup, and the soap containers installed at the car wash.

## Code and Development

Most of the code and YAML was generated with help from ChatGPT. My dad operates the gas station, and I am a full-time student, so using AI helped us move faster and turn the idea into a working system without having to write every piece from scratch.

I still reviewed, tested, adjusted, and applied the code to the real hardware setup. The project was built through trial, testing, and real-world installation at the car wash.

## Repository Contents

This repository includes:

- ESP8266 Arduino code for the VL53L1X soap sensor
- Home Assistant MQTT YAML sensor configuration
- Setup documentation
- Annotated photos of the physical build
- Notes for wiring, installation, and testing

## Current Status

The system is designed as a practical monitoring tool for our car wash. It is not a commercial product, but it is a working custom-built solution for our specific setup.

Future improvements could include:

- Adding more soap containers
- Creating Home Assistant alerts for low soap levels
- Improving calibration
- Building a cleaner dashboard
- Adding long-term usage tracking
- Making the enclosure more durable for daily shop use

## Project Goal

The main goal of this project is simple: make it easier to keep the car wash running smoothly.

By combining a sensor, microcontroller, MQTT, and Home Assistant, we turned a manual maintenance task into something that can be monitored automatically.
