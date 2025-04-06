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

## Issues and Resolutions

During the design and validation process, the following issues were identified and addressed:
- **Issue**: Minor overlap errors in component placement near the USB and button area.
  - **Resolution**: These errors were ignored as per the project instructions, as they did not interfere with functionality or the overall fit of the components inside the housing.
- **Issue**: Antenna placement under components.
  - **Resolution**: The PCB was redesigned to ensure no components or traces were placed beneath the antenna, and the area was cut out as required.

## Conclusion

This project adheres to the design specifications provided, ensuring that all hardware components, such as the ESP32-C6, battery, display, and PCB, fit within the specified mechanical enclosure. The design respects electrical and mechanical constraints, ensuring proper functionality, ease of assembly, and minimal interference.
