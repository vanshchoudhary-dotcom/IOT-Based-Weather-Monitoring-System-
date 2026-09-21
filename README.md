#IoT Based Weather Monitoring System

Overview

The IoT Based Weather Monitoring System is a smart environmental monitoring solution designed to collect and display real-time weather parameters. The system uses multiple sensors to measure temperature, humidity, and rainfall levels and transmits the collected data to the cloud using Wi-Fi. The monitored data is displayed locally on an LCD screen and visualized remotely through ThingSpeak in graphical format.

Features

Real-time temperature monitoring
Real-time humidity monitoring
Rainfall detection and monitoring
LCD display for local data visualization
Wireless data transmission using Wi-Fi
Cloud-based data logging using ThingSpeak
Graphical representation of environmental parameters

Components Used

NodeMCU (ESP8266)
DHT11 Temperature and Humidity Sensor
Rain Sensor Module
16x2 LCD Display (HD44780 Driver)
Power Supply
Jumper Wires

Working Principle

The DHT11 sensor measures temperature and humidity from the surrounding environment.
The rain sensor detects rainfall intensity and rain level.
The NodeMCU (ESP8266) processes the sensor data.
The measured values are displayed on the 16x2 LCD display.
Using the built-in Wi-Fi capability of ESP8266, sensor data is transmitted to the ThingSpeak cloud platform.
ThingSpeak stores the data and generates graphical visualizations for real-time monitoring and analysis.
System Architecture
Sensors (DHT11 + Rain Sensor) | v NodeMCU ESP8266 |
| | v v LCD Display ThingSpeak Cloud | v Graphical Analysis

Applications

Smart Agriculture
Weather Monitoring Stations
Environmental Monitoring
Smart City Projects
Educational and Research Applications

Technologies Used

Embedded C / Arduino IDE
ESP8266 Wi-Fi Module
IoT (Internet of Things)
ThingSpeak Cloud Platform

Results

The system successfully monitors environmental conditions and displays:

Temperature (°C)
Humidity (%)
Rainfall Level
The collected data is uploaded to ThingSpeak, where users can monitor environmental changes through real-time graphs and cloud-based dashboards.
