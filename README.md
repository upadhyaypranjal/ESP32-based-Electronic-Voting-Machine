This repository contains the firmware and documentation for an ESP32-based Electronic Voting Machine (EVM). The system is designed for small-scale elections and integrates IoT capabilities for real-time, remote monitoring of results. It provides a secure, efficient, and transparent alternative to traditional paper-based voting.




Table of Contents
Objective

Features

Hardware Components

Software & Libraries

Pinout & Circuit Diagram

How It Works

Cloud Integration

Setup & Installation

Future Scope

Objective
The primary objective of this project is to create a secure, reliable, and real-time voting system by integrating live vote monitoring via the cloud. It eliminates the need for physical ballots, reduces costs, and automates the counting process to improve speed and accuracy.




Features

Simple Push-Button Voting: An easy-to-use interface with dedicated buttons for each candidate/party.



Instant LCD Feedback: An 8x2 I2C LCD screen displays real-time prompts and voting results.




Live Cloud Monitoring: Utilizes Wi-Fi to transmit final vote counts to the ThingSpeak platform for remote tracking and analysis.



LED Indicators: Onboard LEDs provide immediate visual confirmation for a successfully cast vote and indicate different system states.



Result Finalization: A dedicated button ends the voting process, displays the final tally, and triggers the data upload to the cloud.


Hardware Components
ESP32 Microcontroller with built-in Wi-Fi 

8x2 I2C LCD Display (Address: 

0x27) 


1x Green LED 

1x Red LED 

3x Push Buttons for voting 

1x Push Button for displaying results 

Breadboard and connecting wires

Software & Libraries

IDE: Arduino IDE 


Language: Embedded C++ 

Libraries:


<WiFi.h> (Standard with ESP32 core) 



<Wire.h> (Standard) 


<LiquidCrystal_I2C.h> by Marco Schwartz 


Pinout & Circuit Diagram
Pin Mapping
Component	ESP32 Pin	Description
Green LED	GPIO 14	Blinks to confirm a successful vote has been registered.
Red LED	GPIO 12	Blinks during the result display animation.
Result Button	GPIO 16	Displays final results on the LCD and uploads data to ThingSpeak.
Vote Button Party 1	GPIO 25	Registers one vote for Party 1.
Vote Button Party 2	GPIO 26	Registers one vote for Party 2.
Vote Button Party 3	GPIO 27	Registers one vote for Party 3.
I2C SDA (for LCD)	GPIO 21	The serial data line for I2C communication with the LCD.
I2C SCL (for LCD)	GPIO 22	The serial clock line for I2C communication with the LCD.



Export to Sheets
Circuit Diagram

(Image from the project report) 

How It Works
The operational flow of the system is as follows:


Startup: The system initializes hardware, displays a welcome message ("ELECTRONIC VOTING MACHINE"), and connects to the configured Wi-Fi network.


Voting Loop: It enters the main voting mode, prompting users with "Cast your vote" on the LCD.


Casting a Vote: When a voter presses a party's button, the vote count for that party is incremented. The green LED blinks, and a confirmation ("Voted! Px") is shown on the LCD.


Finalizing Results: When the result button is pressed, an LED animation plays, and further voting is disabled.




Display & Upload: The final results are displayed sequentially on the LCD for each party. The data is then sent to ThingSpeak via an HTTP POST request. A confirmation message, "RESULTS SENT TO CLOUD," is shown.





End of Session: A final "THANK YOU" message is displayed.

Cloud Integration
The EVM uploads the final vote counts for each party to a pre-configured ThingSpeak channel. Each party's total is mapped to a separate field (e.g., Party 1 to Field 1, Party 2 to Field 2). This allows for live, timestamped data visualization and analysis.



Example ThingSpeak Visualization

(Image from the project report) 

Setup & Installation
Hardware Assembly: Connect the components according to the circuit diagram and pinout table.

IDE Setup:

Install the Arduino IDE.

Add the ESP32 board manager to the Arduino IDE.

Install the LiquidCrystal_I2C library using the Library Manager.

Configure Firmware:

Clone this repository.

Open the .ino file in the Arduino IDE.

Update the following lines with your credentials:

C++

// === WiFi credentials ===
const char* ssid = "YOUR_WIFI_SSID"; // [cite: 94]
const char* password = "YOUR_WIFI_PASSWORD"; // [cite: 95]

// === ThingSpeak ===
const char* apiKey = "YOUR_THINGSPEAK_API_KEY"; // [cite: 100]
Upload: Select your ESP32 board and the correct COM port, then upload the code.

Future Scope
The system is designed to be scalable and can be upgraded with future enhancements such as:

Face Recognition or Fingerprint Authentication for voter verification.

Blockchain integration for enhanced security.

Mobile or web application integration for a more comprehensive voting experience.
