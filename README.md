# AI-Powered Drone for Aerial Image Detection

An integrated mechatronics and embedded-systems graduation project for aerial imaging, real-time flight control, wireless telemetry, environmental monitoring, and AI-assisted crop-health analysis.

**Author:** Mohamed Gamal | **Program:** Second-Year Mechatronics, Faculty of Industry and Energy Technology | **University:** New Cairo Technological University

This project was developed as part of my second year in Mechatronics. My responsibilities covered the electronics, communication protocols, IoT subsystem, and the complete transmitter/receiver system, including PCB design, component integration, firmware, wiring, bench testing, and hardware troubleshooting.

## Project demonstration

The full project video presents the drone, its electronics, the flight-control system, and the aerial image-detection concept. These short GIFs provide quick previews; the complete 3-minute recording is linked below.

### Demonstration highlight 1

An excerpt from the project demonstration.
![Drone demonstration highlight](media/gifs/drone-demo-highlight-1.gif)

### Demonstration highlight 2

Another excerpt from the project demonstration.
![Drone demonstration highlight](media/gifs/drone-demo-highlight-2.gif)

### Demonstration highlight 3

A third short excerpt from the project demonstration.
![Drone demonstration highlight](media/gifs/drone-demo-highlight-3.gif)

**Full video:** [AI-Powered Drone demonstration](media/videos/AI-Powered_Drone_Full_Demonstration.mp4)

## System architecture

The project combines a custom quadcopter, wireless manual controls, a flight controller, environmental sensing, and an aerial-imaging pipeline.

| Subsystem | Hardware and implementation |
| --- | --- |
| Flight platform | Quadcopter frame, BLDC motors, electronic speed controllers, APM 2.8 flight controller, servo/control interfaces, power distribution, and onboard electronics |
| Mechanical design | Custom quadcopter frame and mounting components designed in SolidWorks; structural stress analysis and assembly documentation are included |
| Transmitter | ESP32 with dual-axis joysticks, calibration logic, OLED status display, nRF24L01 wireless radio, and two flight-control switches |
| Receiver | Arduino Nano with nRF24L01 radio, PWM/servo outputs for APM 2.8, altitude-hold and stabilize-mode signals, and disarmed safe-output behavior |
| Wireless link | nRF24L01 at channel 76, 1 Mbps data rate, maximum RF power, and a shared `NODE1` RF pipe |
| IoT monitoring | ESP8266, DHT11 temperature/humidity sensor, Wi-Fi access, and Blynk cloud dashboards for Android, iOS, and PC |
| AI and image analysis | Computer vision for drone-based aerial image acquisition, crop-health inspection, and detection support |

## Transmitter

The custom transmitter is based on an ESP32 and reads four calibrated joystick axes:

- Throttle
- Yaw
- Pitch
- Roll

The firmware measures each joystick at the center position, calculates offsets, applies a dead-zone, inverts the throttle where required, and maps the four channels to PWM values from 1000 to 2000 microseconds. An OLED displays the live channel values and switch states.

**Hardware:**

- ESP32
- Dual 2-axis joystick modules
- SSD1306 OLED display
- nRF24L01 wireless transceiver
- Signal/altitude-hold switch
- Flight-mode switch

**Files:** [`firmware/transmitter/Transmitter.ino`](firmware/transmitter/Transmitter.ino)

### Assembled transmitter and PCB

The transmitter PCB brings together the ESP32, joystick modules, nRF24L01 radio, switches, power regulation, and OLED interface.
![Custom transmitter PCB and hardware](hardware/pcb/Transmitter_PNG.png)

### Transmitter PCB routing design

This Proteus PCB layout shows the transmitter board routing and component footprints used to connect the controller, joystick inputs, radio, and display.
![Transmitter PCB routing layout](hardware/pcb/Picture3.png)

## Receiver

The receiver uses an Arduino Nano and an nRF24L01 radio. It listens on the same RF channel and address as the transmitter and converts the received control packet into five servo/PWM channels for the APM 2.8 flight controller:

- Roll
- Pitch
- Throttle
- Yaw
- Flight mode

When the signal switch is inactive, the receiver sends neutral 1000-microsecond outputs for a safe disarmed state.

**Hardware:**

- Arduino Nano
- nRF24L01 wireless transceiver
- Servo/PWM output stage
- APM 2.8 flight-controller inputs
- Receiver and step-down power PCB

**Files:** [`firmware/receiver/Receiver.ino`](firmware/receiver/Receiver.ino)

### Assembled receiver and power board

The receiver PCB combines the Arduino Nano, nRF24L01 radio interface, connectors, and step-down power section for the airborne control link.
![Custom receiver PCB and hardware](hardware/pcb/Reciever_PNG.png)

### Receiver PCB routing design

This Proteus routing view documents the receiver board connections and connector footprints used to pass the radio control channels to the flight controller.
![Receiver PCB routing layout](hardware/pcb/Screenshot%202025-06-26%20160215.png)

## PCB and electronics

The electronics work includes separate transmitter and receiver/step-down PCB designs. The Proteus project files are included for inspecting the board layouts and component connections.

- [Transmitter PCB design](hardware/pcb/MG_Drone_Transmitter.pdsprj)
- [Receiver and step-down PCB design](hardware/pcb/MG_Drone_Reciever&StepDown.pdsprj)

The designs integrate the radio modules, microcontrollers, control switches, joystick/display wiring, PWM outputs, and power regulation. Low-voltage regulation is separated from the flight power path; verify supply rails, grounds, and pin mapping against the assembled hardware before powering it.

## IoT monitoring

An ESP8266 reads temperature and humidity from a DHT11 and publishes the readings to Blynk virtual pins V0 and V1. The project includes mobile and desktop dashboard examples.

**Files:** [`firmware/iot/IOT_final.ino`](firmware/iot/IOT_final.ino)

Before compiling, replace the placeholder Wi-Fi and Blynk credentials in the source.

### Android dashboard

The Android dashboard shows live humidity and temperature gauges and their recent readings.
![Android IoT dashboard](media/photos/iot/Android.jpg)
![Android IoT dashboard](media/photos/iot/Android2.jpg)

### iOS dashboard

The iOS capture documents the mobile monitoring interface for the sensor data.
![iOS IoT dashboard](media/photos/iot/IOS.jpg)

### PC dashboard

The PC dashboard provides a desktop view of the same IoT monitoring project.
![PC IoT dashboard](media/photos/iot/PC.png)

## Mechanical Design and Development

The mechanical work covers the quadcopter frame, its component assembly, and the CAD development workflow. The SolidWorks recording and an optimized GIF preview are provided below.

### SolidWorks design process

This video follows the drone assembly as it is developed and inspected in SolidWorks. The GIF is a short preview; the linked MP4 contains the complete attached design video.
![SolidWorks drone design process](media/gifs/solidworks-design-process.gif)

**Full video:** [SolidWorks drone design process](hardware/design/SolidWorks_Design_Process.mp4)

### Drone model and assembled platform

The rendered model and build photos show the quadcopter frame, motor-arm arrangement, propellers, and mounted electronics.
![SolidWorks-style drone render](media/photos/drone/drone-render.png)
![Drone assembly](media/photos/drone/drone-build.jpg)
![Drone assembly detail](media/photos/drone/drone-build-detail.jpg)

### Structural stress analysis

The included analysis image documents the structural review performed during the mechanical design stage.
![Stress analysis](hardware/design/Stress_Analysis.png)

### Development photos

These photos capture additional stages of prototype assembly and integration.
[Browse development photos](media/photos/development/)

## Launch Exhibition 3 — 3rd place

Our team placed **3rd among Egyptian universities** in mechatronics at the Launch Exhibition 3 competition and received a trophy. The following photos and clips document the project presentation and award moments.

### Project presentation and team photos

These exhibition photos show the drone project display, the award, and the project team.
![Me with my friend and the project award](media/photos/exhibition/friend-and-award.jpg)


### Drone and trophy display

The project drone and competition trophy displayed together at Launch Exhibition 3.
![Drone and trophy display](media/photos/showcase/drone-exhibition-1.jpg)

### Award and trophy GIFs

Short clips from the Launch Exhibition 3 folder highlight the award, trophy reveal, ceremony, and team moments.
![Receiving the trophy](media/gifs/launch-exhibition-award.gif)

![Launch Exhibition team moment](media/gifs/launch-exhibition-team-moment.gif)

**Full video:** [Launch Exhibition award moment](media/videos/Launch_Exhibition_Award_Moment.mp4)

**More photos:** [Launch Exhibition 3 gallery](media/photos/exhibition/)

## Mohamed Gamal — Project and Exhibition

These selected photos identify Mohamed Gamal and document his project presentation, exhibition participation, and hands-on electronics work.

### Presenting the drone

A project-presentation photo of Mohamed Gamal beside the drone and project display.
![Mohamed Gamal presenting the drone project](media/photos/mohamed-gamal/mohamed-gamal-project-presentation.jpg)

### With the project team

Mohamed Gamal pictured with the project team during the exhibition.
![Mohamed Gamal with the project team](media/photos/mohamed-gamal/mohamed-gamal-team.jpg)

### Electronics bench work

Hands-on soldering and electronics assembly during the prototype development.
![Mohamed Gamal working on the electronics](media/photos/mohamed-gamal/mohamed-gamal-soldering.jpg)

### Prototype electronics
This additional image shows the transmitter and receiver electronics during hands-on development.
![Mohamed Gamal prototype bench work](media/photos/mohamed-gamal/mohamed-gamal-bench-work.jpg)

## Institutional recognition

The project was featured by the Ministry of Higher Education and Scientific Research, New Cairo Technological University, and the Technologist Youth Federation.

### Ministry of Higher Education and Scientific Research

The project recognition collage includes media coverage and highlights from the competition.
![Project recognition coverage](media/photos/mohamed-gamal/mohamed-gamal-recognition.jpg)

### New Cairo Technological University

The university's post describing the drone project and its competition result.
![New Cairo Technological University](media/photos/recognition/new-cairo-technological-university.png)

### Union of Technology Youth

A federation feature highlighting the project's smart-agriculture application and student team.
![Union of Technology Youth](media/photos/recognition/technology-youth-federation.png)

## Documentation

The project booklet, poster, and presentations provide the written and visual background for the project.

- [Project booklet PDF](documentation/Drone_Project_Booklet.pdf)
- [Project poster PDF](documentation/Project_Poster.pdf)
- [Main project presentation](documentation/AI-Powered%20Drone%20for%20Aerial%20Image%20Detection.pptx)
- [Business presentation](documentation/AI-Powered%20Drone%20for%20Aerial%20Image%20Detection_Business.pptx)
- [Phase 1 presentation](documentation/Ai_Powerd_Drone_For_Image_Ditection_Phase_1.pptx)
