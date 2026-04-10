# 🗑️ Waste Segregation Dustbin

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](./LICENSE)
[![Platform: Arduino](https://img.shields.io/badge/Platform-Arduino-teal.svg)](https://www.arduino.cc/)
[![Edge Impulse](https://img.shields.io/badge/Powered%20by-Edge%20Impulse-blue.svg)](https://edgeimpulse.com/)
[![Embedded ML](https://img.shields.io/badge/ML-TensorFlow%20Lite-orange.svg)](https://www.tensorflow.org/lite)

An embedded machine-learning system that automatically segregates waste into categories — **wet**, **dry**, and **clear/empty** — using a camera-equipped microcontroller and on-device AI models trained with [Edge Impulse](https://edgeimpulse.com/). The system runs entirely offline on low-power hardware such as an ESP32-CAM or Arduino Nicla Vision, making real-time waste classification accessible and affordable.

---

## 📖 Table of Contents

- [Motivation](#motivation)
- [Features](#features)
- [Project Structure](#project-structure)
- [Datasets](#datasets)
- [Models](#models)
- [Setup & Installation](#setup--installation)
- [Usage](#usage)
- [Results](#results)
- [Roadmap](#roadmap)
- [Contributing](#contributing)
- [License](#license)

---

## 💡 Motivation

Improper waste disposal is a growing environmental problem. Manual sorting is time-consuming and inconsistent. This project demonstrates how tiny Machine Learning (TinyML) can be deployed on inexpensive microcontrollers to build a smart dustbin that automatically identifies waste type and can trigger a mechanical sorting mechanism — no cloud connection required.

---

## ✨ Features

| Feature | Description |
|---|---|
| **Wet / Dry classification** | Distinguishes organic/wet waste from dry recyclable waste using the `wetDry` model |
| **Lab waste classification** | Classifies specific lab waste types using the `LAB_WASTES1` model |
| **Clear / Empty detection** | Detects when the bin view is clear (no waste present) |
| **On-device inference** | All inference runs locally on the microcontroller (no internet required) |
| **Arduino compatible** | Works with ESP32, Arduino Nano 33 BLE Sense, Nicla Vision, Portenta H7, RP2040, Sony Spresense |
| **Serialoutput** | Real-time predictions printed to the Serial Monitor at 115 200 baud |

---

## 🗂️ Project Structure

```
waste-segregation-dustbin/
├── datasets/                        # Image datasets used to train the models
│   ├── drywastePIC/                 # Dry waste images (paper, plastic, cardboard …)
│   ├── wetWastePic/                 # Wet waste images (food scraps, organic matter …)
│   ├── CLEAR/                       # Empty-bin / background images
│   ├── archives/                    # Backup zip files and original downloads
│   └── README.md                    # Dataset documentation
├── edge-impulse-libraries/          # Exported Arduino inference libraries
│   ├── LAB_WASTES1_inferencing/     # Lab-waste classifier (v1.0.3)
│   ├── wetDry_inferencing/          # Wet/Dry classifier (v1.0.1)
│   └── README.md                    # Library usage guide
├── LICENSE                          # MIT License
└── README.md                        # This file
```

---

## 📦 Datasets

The `datasets/` directory contains the image data used to train and validate the ML models. Images were collected using mobile phone cameras and development board cameras (Nicla Vision, ESP32-CAM, etc.).

### Classes

| Folder | Class Label | Description |
|---|---|---|
| `drywastePIC/` | `dry` | Paper, plastic, cardboard, and other dry recyclables |
| `wetWastePic/` | `wet` | Food scraps, organic matter, and other wet waste |
| `CLEAR/` | `clear` | Empty bin or plain background (no waste) |

### Labeling Scheme

Images are organized **per folder** — the folder name is used directly as the class label when uploading to Edge Impulse. No separate annotation file is needed.

### Uploading to Edge Impulse

1. Log in to [Edge Impulse Studio](https://studio.edgeimpulse.com/).
2. Open (or create) your project.
3. Go to **Data acquisition → Upload data**.
4. Select all images from a class folder (e.g. `drywastePIC/`).
5. Set the **label** to match the folder name (`dry`, `wet`, or `clear`).
6. Repeat for each class.

> See [`datasets/README.md`](./datasets/README.md) for full details.

---

## 🧠 Models

Two Edge Impulse models are provided as pre-built Arduino libraries:

### 1. `wetDry_inferencing` (v1.0.1)

Classifies incoming camera frames as either **Wet** or **Dry** waste.

- **Input**: Image (camera frame)
- **Output classes**: `wet`, `dry`
- **DSP block**: Image processing
- **ML block**: Neural network (TensorFlow Lite for Microcontrollers)

### 2. `LAB_WASTES1_inferencing` (v1.0.3)

A more detailed classifier targeting **lab waste** types.

- **Input**: Image (camera frame)
- **Output classes**: Multiple lab-waste categories (see Serial Monitor output for class names)
- **DSP block**: Image processing
- **ML block**: Neural network (TensorFlow Lite for Microcontrollers)

Both models run entirely on-device using the Edge Impulse inference SDK — no cloud calls at runtime.

> See [`edge-impulse-libraries/README.md`](./edge-impulse-libraries/README.md) for installation and usage.

### Training Approach (High-level)

1. Collect labelled images (see [Datasets](#datasets)).
2. Upload to Edge Impulse Studio and split into training / test sets.
3. Create an **Impulse**: Image → DSP block → Neural Network classifier.
4. Train the neural network (transfer learning or custom architecture available in Studio).
5. Test accuracy on the held-out set.
6. Export the trained model as an **Arduino library** (`.zip`).
7. Unzip into the Arduino `libraries/` folder and deploy to hardware.

---

## 🔧 Setup & Installation

### Prerequisites

| Tool | Purpose |
|---|---|
| [Arduino IDE 2.x](https://www.arduino.cc/en/software) | Compile and upload sketches |
| [Edge Impulse CLI](https://docs.edgeimpulse.com/docs/edge-impulse-cli) *(optional)* | Re-train or update models |
| Compatible board | ESP32, Nano 33 BLE Sense, Nicla Vision, Portenta H7, RP2040, or Sony Spresense |

### Installing an Inference Library

1. Clone this repository (or download the ZIP):
   ```bash
   git clone https://github.com/Sndcooper/waste-segregation-dustbin.git
   ```

2. Copy the desired library folder into your Arduino libraries directory:
   ```bash
   # macOS / Linux
   cp -r edge-impulse-libraries/wetDry_inferencing ~/Arduino/libraries/

   # Windows (PowerShell)
   Copy-Item -Recurse edge-impulse-libraries\wetDry_inferencing "$env:USERPROFILE\Documents\Arduino\libraries\"
   ```

3. Restart the Arduino IDE so it picks up the new library.

4. Install any board-specific sensor libraries via **Tools → Manage Libraries** (e.g. `Arduino_OV767X` for camera boards).

---

## 🚀 Usage

### Running an Example Sketch

1. Open the Arduino IDE.
2. Go to **File → Examples → wetDry_inferencing** (or `LAB_WASTES1_inferencing`).
3. Choose the sub-example that matches your board and sensor (e.g. `esp32 / camera`).
4. Select your board under **Tools → Board** and the correct **Port**.
5. Click **Upload** (⟶).
6. Open **Tools → Serial Monitor** and set the baud rate to **115200**.

### Expected Serial Output

```
Predictions (DSP: 15 ms., Classification: 30 ms., Anomaly: 0 ms.):
    wet: 0.88
    dry: 0.12
```

The prediction with the highest probability is the detected waste category. You can use this output to trigger GPIO pins (e.g. open a servo to route the waste into the correct bin compartment).

### Triggering a Sorting Mechanism (Example Logic)

```cpp
if (result.classification[ix].value > 0.7) {
    String label = result.classification[ix].label;
    if (label == "wet") {
        digitalWrite(WET_BIN_SERVO_PIN, HIGH);
    } else if (label == "dry") {
        digitalWrite(DRY_BIN_SERVO_PIN, HIGH);
    }
}
```

---

## 📊 Results

> **TODO**: Add confusion matrix, accuracy metrics, and sample prediction screenshots after running the model evaluation in Edge Impulse Studio.

### How to Evaluate

1. In Edge Impulse Studio, go to **Model testing**.
2. Click **Classify all** to run inference on the test set.
3. Review the **Confusion Matrix** and **F1 score** for each class.
4. Export the results and paste them here.

| Model | Accuracy | Notes |
|---|---|---|
| `wetDry_inferencing` v1.0.1 | _TODO_ | Test on held-out dataset |
| `LAB_WASTES1_inferencing` v1.0.3 | _TODO_ | Test on held-out dataset |

---

## 🗺️ Roadmap

- [ ] Add more diverse training images (different lighting, angles, waste types)
- [ ] Expand lab waste classes in `LAB_WASTES1` model
- [ ] Add a hardware wiring diagram / schematic
- [ ] Integrate servo control code for the physical sorting mechanism
- [ ] Add a mobile / web dashboard for monitoring bin fill levels
- [ ] Publish a detailed build guide (PCB, enclosure, BOM)
- [ ] Support additional boards (Raspberry Pi Pico W, XIAO ESP32S3)

---

## 🤝 Contributing

Contributions are welcome! Here's how to get started:

1. Fork the repository.
2. Create a new branch: `git checkout -b feature/your-feature-name`.
3. Make your changes and commit: `git commit -m "Add your feature"`.
4. Push to your fork: `git push origin feature/your-feature-name`.
5. Open a Pull Request describing your changes.

Please keep PRs focused and include a short description of what you changed and why.

---

## 📄 License

This project is licensed under the **MIT License** — see the [LICENSE](./LICENSE) file for details.

Copyright © 2026 [Sndcooper](https://github.com/Sndcooper)
