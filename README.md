# EEG-Signal-Visualization-using-Arduino-Python


This project captures and visualizes EEG (electroencephalography) signals using an Arduino and Python. The EEG data is collected from an analog sensor, transmitted via serial communication, and plotted in real-time.

## Table of Contents
- [Introduction](#introduction)
- [Features](#features)
- [Hardware Requirements](#hardware-requirements)
- [Software Requirements](#software-requirements)
- [Setup Instructions](#setup-instructions)
- [Usage](#usage)
- [Example Output](#example-output)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)
- [License](#license)

## Introduction
This project is designed for capturing brain wave signals using an EEG sensor connected to an Arduino. The captured signal is sent to a Python script via serial communication, which then visualizes the data using Matplotlib.

## Features
- Real-time EEG data acquisition
- Graphical visualization of EEG signals
- Adjustable sampling rate
- Simple and lightweight code

## Hardware Requirements
- Arduino (Uno, Mega, etc.)
- EEG Sensor
- Jumper Wires
- USB Cable for Arduino

## Software Requirements
- Arduino IDE
- Python 3.x
- Required Python Libraries:
  - `pyserial`
  - `matplotlib`

## Setup Instructions
### Arduino Setup
1. Connect the EEG sensor to the Arduino.
2. Use the following Arduino code:
   ```cpp
   int eegPin = A5;  // Assign the analog pin
   void setup() {
       Serial.begin(9600);  // Initialize serial communication
   }
   void loop() {
       int eegValue = analogRead(eegPin);  // Read the EEG signal
       Serial.println(eegValue);  // Send the value to the serial monitor
       delay(1);  // Adjust as necessary
   }
   ```
3. Upload the code to the Arduino board using the Arduino IDE.

### Python Setup
1. Install the required Python libraries using:
   ```sh
   pip install pyserial matplotlib
   ```
2. Save the following Python script:
   ```python
   import serial
   import matplotlib.pyplot as plt
   ser = serial.Serial('COM15', 9600)  # Replace 'COM15' with your Arduino port
   eeg_data = []
   plt.ion()
   fig, ax = plt.subplots()
   while True:
       data = ser.readline().strip()
       try:
           eeg_value = int(data)
           eeg_data.append(eeg_value)
           if len(eeg_data) > 100:  # Keep last 100 samples
               eeg_data.pop(0)
           ax.clear()
           ax.plot(eeg_data)
           plt.pause(0.01)
       except:
           continue
   ```
3. Run the script with:
   ```sh
   python eeg_visualization.py
   ```

## Example Output
![EEG Graph Example](example_graph.png)

## Troubleshooting
- **No data received?** Check the Arduino serial port and baud rate.
- **Graph not updating?** Ensure Python and Matplotlib are properly installed.
- **Data is noisy?** Try adding a low-pass filter to the software or using shielded cables.

## Contributing
Contributions are welcome! Feel free to fork the repository and submit a pull request.

## License
This project is licensed under the MIT License.

