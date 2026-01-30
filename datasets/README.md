# Datasets

This directory contains the image datasets used for training and testing the machine learning models.

## 📂 Directory Structure

### 1. [drywastePIC](./drywastePIC)
*   **Description**: Contains images of dry waste items (e.g., paper, plastic, cardboard).
*   **Usage**: Used to train the "Dry" class in the `wetDry` classifier or waste type classifier.

### 2. [wetWastePic](./wetWastePic)
*   **Description**: Contains images of wet waste items (e.g., food scraps, organic matter).
*   **Usage**: Used to train the "Wet" class in the waste classifier.

### 3. [CLEAR](./CLEAR)
*   **Description**: Contains images of the empty bin or clear background.
*   **Usage**: Used as a background class or to detect when the bin is empty.

### 4. [archives](./archives)
*   **Description**: Contains backup zip files and original downloads.
*   **Contents**:
    *   `ei-lab_wastes1-arduino-1.0.3.zip`: Original library archive.
    *   `images_of_CLEAR.zip`: Backup of the CLEAR dataset.

## 📝 Data Collection Info
These images are typically collected using:
*   Mobile phone cameras
*   Development board cameras (like Nicla Vision or ESP32-CAM)

## ☁️ Uploading to Edge Impulse
To add more data to your project:
1.  Navigate to the **Data acquisition** tab in your Edge Impulse project.
2.  Click **Upload data**.
3.  Select the images from these folders.
4.  Label them according to their folder name (e.g., `wet`, `dry`, `clear`).
