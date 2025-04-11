# Engineering Validation (EVT) - PCB and Mechanical Design

## Project Overview

This project focuses on the design and validation of a printed circuit board (PCB) for an electronic device that includes various components like an ESP32-C6 module, battery, display, and mechanical housing. The goal is to ensure that the PCB fits within the given mechanical enclosure, adheres to specified electrical and mechanical constraints, and follows best practices for power routing, component placement, and design rules.

## Project Structure

- **Hardware**
  - **Schematic File** (`.sch`)
  - **PCB Layout File** (`.brd`)
- **Manufacturing**
  - **Gerbers** (`gerbers.zip`)
  - **Bill of Materials** (`.bom`)
  - **Pick and Place File** (`.cpl`)
- **Mechanical**
  - **3D Model of Complete Device** (exploded view `.step`)
  - **Fusion 360 3D Model** (assembled device)
- **Images**
  - Renders of the device, PCB, and individual components
- **LICENSE**
  - License information
- **README.md**
  - This file, describing the project

## Design Decisions and Functional Overview

### 1. **Schematic Design**
The schematic was designed according to the provided model and constraints. Key considerations included ensuring proper placement of decoupling capacitors close to the power pins of critical components, maintaining correct power and data routing widths, and keeping signal integrity intact.

- **Power Routing**: Power traces were routed with a minimum width of `0.3mm` for power rails (e.g., VCC, VBUS) and `0.15mm` for signal traces.
- **Component Placement**: All components were placed on the **TOP** layer of the PCB, with key modules grouped around the central ESP32-C6 microcontroller. The placement adhered to the mechanical dimensions of the housing.
- **Stacked Ground Planes**: Ground planes were created both on the **TOP** and **BOTTOM** layers, and via stitching was applied near the ESP32 module to ensure minimal noise.

### 2. **PCB Layout and Constraints**
Following the provided layout file, I ensured the PCB design adhered to all mechanical and electrical constraints, including:
- **Fitment with Housing**: The PCB was designed to fit inside the provided mechanical enclosure, and critical components such as buttons and USB connectors were positioned as per the specified dimensions.
- **ESP32 Antenna**: The antenna of the ESP32 module was placed near the outer edge of the PCB, and the area beneath it was cut out to minimize interference with the radio signal.
- **Double-sided Routing**: While routing was done on both the **TOP** and **BOTTOM** layers, I avoided vias on power traces and ensured that no signals were routed under the ESP32 antenna.
  
### 3. **Gerber Files**
Gerber files were generated to provide the necessary information for PCB manufacturing. I used the standard process outlined in the provided tutorial to generate the following:
- **Gerber Files** for PCB manufacturing
- **Bill of Materials** (BOM) for procurement
- **Pick and Place File** for component placement during assembly

### 4. **Mechanical Model**
The 3D model of the complete device, including the PCB, battery, display, and housing, was created in Fusion 360. The exploded view `.step` file shows the assembly process and how the components fit within the housing. The models for the battery and display were drawn according to their respective datasheets to ensure accurate dimensions.

- **Battery and Display Integration**: The battery was directly connected to the PCB's test pads, and the display was integrated according to its specified connections.

## Design Rule Check (DRC) and Electrical Rule Check (ERC)

The design was thoroughly checked using the DRC and ERC files provided in the project resources. All electrical and mechanical design constraints were respected, and the following issues were resolved:
- **Power trace widths** and **component placement** were validated.
- **Test pads** were clearly marked in the silkscreen layer with their corresponding signal names (e.g., MISO, MOSI, GND).
- **Via stitching** was applied to ensure proper grounding, particularly around the ESP32 module.

### 5. **Components Used in Mechanical and Electrical Integration**

The following key components were integrated into the design, both electrically on the PCB and mechanically within the Fusion 360 model. Each part was selected based on its functionality, size constraints, and compatibility with the ESP32-C6 ecosystem.

#### **Microcontroller Unit (MCU)**
- **ESP32-C6-WROOM-1-N1 (U2)**  
  A high-performance wireless module with integrated Wi-Fi and Bluetooth LE capabilities. This module acts as the central processing unit, managing connectivity, data handling, and control tasks for the entire device.

#### **Power Supply and Management**
- **USB-C Connector**  
  Primary power input for the device, allowing both power delivery and data communication.
- **LDO Voltage Regulator – XC6220A331MR-G (IC4)**  
  Ensures stable voltage for sensitive components, converting input power to regulated 3.3V.
- **Battery Charging IC – MCP73831**  
  Handles safe charging of a single-cell Li-Po battery, enabling portable operation.
- **Fuel Gauge – MAX17048G+T10 (U4)**  
  Monitors battery voltage and provides state-of-charge estimation for accurate power management.

#### **Memory and Data Storage**
- **External NOR Flash – W25Q512JVEIQ (U1)**  
  Non-volatile memory used to store logs, firmware updates, or configuration data.
- **MicroSD Card Slot**  
  Provides removable storage capability, useful for storing larger datasets or logs.

#### **Real-Time Clock (RTC)**
- **RTC Module – DS3231SN (U3)**  
  Maintains accurate timekeeping, even during power loss. A supercapacitor (C10) is included to retain time data temporarily when external power is disconnected.

#### **Environmental Sensing**
- **BME688 Sensor**  
  Measures temperature, humidity, pressure, and gas, providing rich environmental data for various applications.

#### **User Interface**
- **E-Paper Display**  
  A low-power screen for displaying information clearly and efficiently. Connected via a flat flex connector (`FH34SR-24S-0.5SH_99`) and supported by driver circuitry on the PCB.
- **Buttons (Boot, Reset, Change)**  
  Physical interface elements allowing users to interact with the system, perform resets, or trigger mode changes.

#### **Communication Interfaces**
- **Wireless Connectivity via ESP32-C6**  
  Native support for Wi-Fi 6 and Bluetooth LE enables fast, efficient communication with external devices or networks.

#### **Protection and Debugging**
- **ESD Protection – USBLC6-2SC6Y, PEMF050.1**  
  Safeguards sensitive components against electrostatic discharge from USB or other user-accessible interfaces.
- **Test Pads**  
  Strategically placed signal pads facilitate in-circuit testing and debugging during development or production.

#### **Expandability**
- **Qwiic/Stemma QT Connector**  
  Provides a plug-and-play I2C expansion port for easily integrating additional sensors or peripherals.

### 6. **MCU ESP32 Pins**

The ESP32-C6-WROOM-1 module was integrated as the core processing and communication unit. Its pinout was utilized to support a range of subsystems within the device. The following is an overview of how specific pins were used and organized in the design:

#### **Antenna Placement**
The ESP32-C6 features an integrated PCB antenna located at the end of the module. In this design, the antenna was placed along the outer edge of the PCB to maximize RF performance. A cutout was added beneath the antenna to reduce signal interference from copper traces or ground planes, ensuring reliable wireless communication.

#### **Power Pins**
- `3V3` and `GND` pins were used to supply and stabilize power to the ESP32 module.
- Proper decoupling capacitors were placed near these pins to minimize voltage fluctuations.

#### **USB Communication**
- USB data lines (`D+`, `D−`) were routed to the USB-C connector through ESD protection components, enabling USB-based programming and power delivery.

#### **SD Card Interface**
- Pins such as `CMD`, `CLK`, and `DAT0–DAT2` were connected to the MicroSD card slot to support external storage over an SDIO interface.

#### **SPI Communication**
- The SPI bus (`CS`, `SCK`, `MOSI`, `MISO`) was connected to the external flash memory (W25Q512JVEIQ) for fast, non-volatile storage access.

#### **I2C Bus**
- Two dedicated pins (`SDA`, `SCL`) were used to establish I2C communication with peripherals like the RTC (DS3231SN), environmental sensor (BME688), and the Qwiic/Stemma QT expansion port.

#### **GPIO Usage**
- Multiple GPIOs were assigned to handle:
  - **User Inputs**: Buttons such as Boot, Reset, and Change.
  - **Display Control**: Interface signals for driving the E-Paper display.
  - **Debug/Test Access**: Certain unused GPIOs were routed to test pads for development and troubleshooting.

All unused or unassigned GPIOs were kept accessible where possible for future flexibility.

## Issues and Resolutions

During the design and validation process, the following issues were identified and addressed:
- **Issue**: Minor overlap errors in component placement near the USB and button area.
  - **Resolution**: These errors were ignored as per the project instructions, as they did not interfere with functionality or the overall fit of the components inside the housing.
- **Issue**: Antenna placement under components.
  - **Resolution**: The PCB was redesigned to ensure no components or traces were placed beneath the antenna, and the area was cut out as required.

## Conclusion

This project adheres to the design specifications provided, ensuring that all hardware components, such as the ESP32-C6, battery, display, and PCB, fit within the specified mechanical enclosure. The design respects electrical and mechanical constraints, ensuring proper functionality, ease of assembly, and minimal interference.
