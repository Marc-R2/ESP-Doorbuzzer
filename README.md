# Doorbell ESP-Home Project

This project uses an ESP8266 or ESP32 microcontroller with the [ESP-Home](https://esphome.io/) firmware to create a doorbell with the following features:

- Doorbell button: Press the button to trigger a buzzer sound on the device.
- OTA updates: Update the device over the air (OTA) using a simple web interface or API endpoint.
- Password protection: Set a password for the device's API endpoints to secure them.
- Password change: Change the password for the device's API endpoints through the web interface or API endpoint.

## Getting Started

To get started with this project, you will need the following:

- An ESP8266 or ESP32 microcontroller
- A breadboard and jumper wires
- A buzzer
- A push button

1. Connect the buzzer and button to the microcontroller according to the following diagram:

```
Button -> ESP8266/ESP32
Buzzer -> ESP8266/ESP32
```


2. Flash the ESP-Home firmware onto the microcontroller using the [ESP-Home Flasher tool](https://esphome.io/guides/flashing.html).

3. Create a new ESP-Home project using the [ESP-Home web dashboard](https://esphome.io/guides/getting_started_dashboard.html) and copy the following code into the project's `script.yaml` file:

```yaml
esphome:
  name: doorbell
  platform: ESP8266
  board: esp01_1m

api_password:
  password: !secret
    current_password: "admin"

# Replace the following with your WiFi credentials
wifi:
  ssid: "YourWifiName"
  password: "YourWifiPassword"

# Perform an OTA update when the device is first booted
on_boot:
  - update.download:
      url: https://raw.githubusercontent.com/Marc-R2/ESP-Doorbuzzer/master/script.yaml
      headers:
        User-Agent: "ESP-Home"
  - system.restart
```

