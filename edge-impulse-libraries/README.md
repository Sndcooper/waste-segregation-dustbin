# Edge Impulse Libraries

This directory contains Arduino libraries exported from your Edge Impulse projects.
These libraries allow you to run your trained Machine Learning models directly on microcontrollers (Arduino, ESP32, etc.).

## 📂 Libraries Included

### 1. [LAB_WASTES1_inferencing](./LAB_WASTES1_inferencing)
*   **Purpose**: Classification of Lab Waste types.
*   **Version**: 1.0.3
*   **Supports**: ESP32, Nano 33 BLE Sense, Nicla Vision, Portenta H7, RP2040, Sony Spresense.
*   [Read Full Guide](./LAB_WASTES1_inferencing/README.md)

### 2. [wetDry_inferencing](./wetDry_inferencing)
*   **Purpose**: Distinguishing between Wet and Dry waste.
*   **Version**: 1.0.1
*   **Supports**: ESP32, Nano 33 BLE Sense, Nicla Vision, Portenta H7, RP2040, Sony Spresense.
*   [Read Full Guide](./wetDry_inferencing/README.md)

## 🛠️ General Usage Guide

To use any of these libraries in your project:

1.  **Install**: Move the library folder into your Arduino libraries directory (e.g., `Documents/Arduino/libraries/`).
2.  **Restart**: Restart the Arduino IDE.
3.  **Examples**: Open **File > Examples > {Library Name}** to see code specific to your board and sensor.
4.  **Hardware**: Ensure your sensors (camera/microphone/accelerometer) are connected properly.
5.  **Build**: Select your board in **Tools > Board** and upload the sketch.
6.  **Monitor**: Use the **Serial Monitor** at **115200 baud** to see real-time classification results.

## 🔗 Resources
*   [Edge Impulse Documentation](https://docs.edgeimpulse.com/)
*   [Arduino Library Usage Guide](https://docs.arduino.cc/software/ide-v1/tutorials/installing-libraries)
