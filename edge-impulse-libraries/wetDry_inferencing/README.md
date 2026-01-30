# wetDry_inferencing

**Version:** 1.0.1  
**Author:** EdgeImpulse Inc.

This is an Arduino library exported from Edge Impulse for the project **wetDry**.

## 🧠 What It Does
This library contains a pre-trained Machine Learning model designed to distinguish between **Wet** and **Dry** waste. It runs entirely on-device (Edge AI).

It includes:
- **Digital Signal Processing (DSP)** blocks to process raw sensor data.
- **Neural Network (NN)** model (TensorFlow Lite for Microcontrollers) to classify the processed data.
- **Inference Engine** to run the model efficiently on embedded hardware.

It takes raw input (typically images in this context, or sensor data) and outputs a probability score predicting if the waste is Wet or Dry.

## 🚀 How to Use

### 1. Installation
1.  **Copy Folder**: Ensure this folder (`wetDry_inferencing`) is located inside your Arduino `libraries` folder (usually found at `Documents/Arduino/libraries/`).
2.  **Restart IDE**: If the Arduino IDE is currently open, restart it to load the new library.

### 2. Running an Example
The library comes with pre-built examples for various development boards.

1.  Open the Arduino IDE.
2.  Go to **File > Examples > wetDry_inferencing**.
3.  Select your board architecture (e.g., `nano_ble33_sense`, `esp32`, `nicla_vision`).
4.  Select the sensor type matching your hardware setup (e.g., `camera`).
    *   *Note: Ensure your camera module is correctly connected if using an external one.*

### 3. Dependencies
Depending on the example you run, you may need to install specific sensor libraries via the Arduino Library Manager. For example:
- **Camera**: Requires `Arduino_OV767X` or board-specific camera libraries (like `ESP32 Camera`).

### 4. Viewing Results
1.  Connect your board via USB.
2.  Select the correct Port and Board in **Tools**.
3.  Click **Upload**.
4.  Once uploaded, open the **Serial Monitor** (**Tools > Serial Monitor**).
5.  Set the baud rate to **115200**.
6.  The board will continuously capture data and print predictions:
    ```text
    Predictions (DSP: 15 ms., Classification: 30 ms., Anomaly: 0 ms.):
    Wet: 0.88
    Dry: 0.12
    ```
