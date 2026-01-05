# Simple2S2C Battery Pack Schematic Description

## Overview
This document describes the schematic design for a 2S LiFePO4 battery pack with integrated temperature monitoring and protection.

## Main Components

### Battery Cells
- **Type**: Calb DTP803450 LiFePO4 cells
- **Configuration**: 2S (2 cells in series)
- **Nominal Voltage**: 3.2V per cell (6.4V total)
- **Quantity**: 2

### Battery Protection IC
- **Part**: BQ29209
- **Function**: Overvoltage, undervoltage, and overcurrent protection
- **Features**:
  - 2-series cell Li-ion/LiFePO4 battery protection
  - Precision voltage monitoring
  - Temperature monitoring via NTC thermistor
  - I2C interface for configuration and monitoring

### Temperature Sensors

#### NTC Thermistor (for BQ29209)
- **Type**: NTC (Negative Temperature Coefficient) thermistor
- **Connection**: Connected to BQ29209 TS (Temperature Sense) pin
- **Power Source**: Battery pack
- **Function**: Critical temperature detection for battery protection

#### TMP117 Digital Temperature Sensor
- **Interface**: I2C
- **Power Source**: External (NOT from battery pack)
- **Function**: Precision temperature monitoring
- **Features**:
  - High-accuracy digital temperature sensor
  - I2C interface
  - Low power consumption

### Thermal Management
- **Component**: Thin PCB or silicone thermal pad
- **Function**: Heat distribution and monitoring
- **Interface**: Separate pins to header

## Connections

### Main Header Pinout
The main header provides the following connections:

1. **Power Connections**:
   - VBAT+ (Battery positive output)
   - VBAT- / GND (Battery negative / Ground)
   - VIN+ (Charging input positive)
   - VIN- / GND (Charging input negative)

2. **I2C Bus**:
   - SCL (Serial Clock)
   - SDA (Serial Data)
   - Connected to BQ29209 (if I2C capable) and TMP117

3. **TMP117 Connections**:
   - VDD (External power supply)
   - GND (Ground)
   - SCL (I2C Clock)
   - SDA (I2C Data)

4. **Thermal Pad Connections**:
   - Thermal sense pins
   - Ground reference

## Circuit Description

### Battery Protection Path
1. Battery cells (2x DTP803450) connected in series
2. Series stack connected to BQ29209 for voltage monitoring
3. NTC thermistor mounted near cells, connected to BQ29209 TS pin
4. BQ29209 controls charge/discharge FETs based on voltage, current, and temperature
5. Protected output to VBAT+ and VBAT- on header

### Temperature Monitoring
1. **Primary (NTC)**: Direct thermal monitoring for protection
2. **Secondary (TMP117)**: High-precision I2C temperature monitoring with external power
3. **Thermal Pad**: Physical thermal interface for heat spreading

### Power Distribution
- Battery pack powers: BQ29209, NTC sensor, load via header
- External power required for: TMP117
- All grounds are common

## Assembly Variant-1
This is the base configuration including:
- 2x Calb DTP803450 cells
- BQ29209 protection IC
- NTC thermistor
- TMP117 temperature sensor (externally powered)
- Thermal pad with header connections
- Main header with all connections
