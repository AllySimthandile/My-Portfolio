This project demonstrates how to use fuzzy logic to control a machine based on temperature and humidity levels. The system uses sensors (DHT22) connected to a Raspberry Pi and a relay module to manage the machine's state. If the temperature and humidity exceed certain thresholds, the system will activate or deactivate the machine accordingly.

This code includes mocking of sensor libraries when running on Windows, making it suitable for both testing and real-world applications on a Raspberry Pi.

Prerequisites
Before running the script, ensure you have the following Python libraries installed:

numpy (for numerical operations)
skfuzzy (for fuzzy logic operations)
matplotlib (for generating fuzzy membership function plots)
RPi.GPIO (for controlling the GPIO pins on Raspberry Pi)
Adafruit_DHT (for reading temperature and humidity sensors)
You can install these dependencies using pip:

bash
Copy code
pip install numpy skfuzzy matplotlib Adafruit-DHT RPi.GPIO
Windows Users:
If you're running this on a Windows machine (for testing purposes), the Adafruit_DHT and RPi.GPIO libraries are mocked, so no hardware interaction will occur. You can test the fuzzy logic portion of the code, but actual hardware control will not be possible on Windows.

Project Overview
This project uses fuzzy logic to control a machine based on the values of temperature and humidity:

Input Variables:

Temperature: Input is divided into three fuzzy categories: cold, warm, and hot.
Humidity: Input is divided into two fuzzy categories: low and high.
Output Variables:

Comfort: The system calculates the comfort level based on temperature and humidity, which determines whether a machine should be turned on or off.
Fuzzy Logic:

The system uses Gaussian membership functions for temperature and humidity inputs.
The comfort level is determined by a set of fuzzy rules, such as:
If temperature is hot and humidity is low, the comfort is low.
If temperature is warm, the comfort is average.
If temperature is warm and humidity is high, the comfort is very high.
Machine Control:

Based on the calculated comfort level, the system uses a relay to turn on or off a machine.
A relay is controlled using the Raspberry Pi’s GPIO pins.
Features
Sensor Integration: Reads temperature and humidity values from a DHT22 sensor.
Fuzzy Logic: Implements fuzzy membership functions to categorize temperature and humidity.
Machine Control: Uses GPIO pins to control a relay that turns on/off a machine.
Visualization: Plots and saves fuzzy membership functions for both temperature and humidity.
Mocking for Windows: Mocks the sensor libraries (Adafruit_DHT, RPi.GPIO) when running on Windows for testing.
Usage
Running on Raspberry Pi or Compatible Platform
Setup:

Connect the DHT22 sensor to the Raspberry Pi (or compatible device).
Connect a relay module to control the machine, using GPIO pin 26.
Run the Script: Save the script as Temp-HumiditySensing.py and execute it:

bash
Copy code
python Temp-HumiditySensing.py
The script will:

Read the temperature and humidity values from the DHT22 sensor.
Normalize the values to a range between 0 and 1.
Apply fuzzy logic rules to calculate the comfort level.
Control the machine (via GPIO) based on the comfort level.
Outputs:

The system will print temperature and humidity readings along with their corresponding fuzzy membership values.
It will print whether the machine is turned on or off based on the fuzzy logic result.
Stopping the Program:

The program can be stopped by pressing Ctrl+C. The relay will be turned off, and the GPIO cleanup will be done.
Running on Windows (Mocking Libraries)
For testing the fuzzy logic without actual hardware interaction, run the script on a Windows machine. The Adafruit_DHT and RPi.GPIO libraries will be mocked, and simulated sensor readings will be used. This allows you to focus on the logic and visualization portions of the code.

Plotting Membership Functions
The script will generate and save a plot of the fuzzy membership functions for temperature and humidity. The image will be saved as fuzzy_mem_temp_hum.png.

The plot will show:

Temperature categories: cold, warm, hot
Humidity categories: low, high
You can view this image to understand how the fuzzy membership functions are defined for the inputs.

Example Output (Terminal)
bash
Copy code
initialization...
saving membership...
done
program is ready for making decision based fuzzy logic
sensing...
Sensing: Temperature=22.5*C Humidity=75.0%
Normalization: Temperature=0.3750 Humidity=0.7500
fuzzy membership: Temperature={'cold': 0.0000, 'warm': 0.9999, 'hot': 0.0000} Humidity={'low': 0.0000, 'high': 1.0000}
comfort level: 20.897
a machine already turn on
Pin Configuration
Relay Pin: GPIO pin 26 (can be changed in the script)
DHT22 Pin: GPIO pin 23 (can be changed in the script)
Customizing the Code
Temperature and Humidity Categories: Modify the Gaussian and trapezoidal membership functions to suit different sensor ranges.
Fuzzy Rules: Add or adjust the fuzzy rules for different comfort levels.
GPIO Pin: Change the GPIO pin for the relay by updating the relay_pin variable.
