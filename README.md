# Simple2S2C Battery Pack

A 2-series (2S) LiFePO4 battery pack with integrated protection, temperature monitoring, and thermal management.

## Overview

Simple2S2C is a battery pack design using two Calb DTP803450 LiFePO4 cells with comprehensive protection and monitoring features. The design includes the BQ29209 battery protection IC, dual temperature sensing, and a thermal management system.

## Key Features

### Battery System
- **Cells**: 2x Calb DTP803450 LiFePO4 cells in series
- **Nominal Voltage**: 6.4V (3.2V per cell)
- **Maximum Voltage**: 7.3V (3.65V per cell)
- **Chemistry**: LiFePO4 (safer, longer life)

### Protection
- **IC**: BQ29209 2-series battery protection controller
- **Features**:
  - Overvoltage protection (OVP)
  - Undervoltage protection (UVP)
  - Overcurrent protection (OCP)
  - Short circuit protection (SCP)
  - Temperature protection via NTC thermistor

### Temperature Monitoring
- **Primary**: NTC thermistor connected to BQ29209 for critical temperature detection
- **Secondary**: TMP117 high-accuracy I2C temperature sensor (externally powered)
- **Thermal Management**: Thin PCB or silicone thermal pad with header interface

### Interfaces
- **Main Header**: Consolidates all connections
  - Ground and Power (in/out)
  - I2C bus (SCL, SDA)
  - TMP117 external power pins
  - Thermal pad sensing pins

## Documentation

Detailed documentation is available in the `docs/` directory:

- **[SCHEMATIC.md](docs/SCHEMATIC.md)**: Schematic description and circuit design
- **[BOM.md](docs/BOM.md)**: Bill of Materials for Variant-1
- **[COMPONENTS.md](docs/COMPONENTS.md)**: Detailed component specifications
- **[PINOUT.md](docs/PINOUT.md)**: Main header pinout and signal descriptions
- **[VARIANT-1.md](docs/VARIANT-1.md)**: Assembly documentation for Variant-1

## Assembly Variants

### Variant-1 (Current)
The baseline configuration including:
- 2x Calb DTP803450 LiFePO4 cells
- BQ29209 protection IC with NTC thermistor
- TMP117 temperature sensor (externally powered)
- Thermal pad with header connections
- Main header with all interfaces

## Important Notes

1. **TMP117 Power**: The TMP117 temperature sensor is **NOT** powered by the battery pack. External power supply is required.

2. **I2C Bus**: Both the BQ29209 (if equipped with I2C) and TMP117 share the same I2C bus accessible via the main header.

3. **Thermal Contact**: The NTC thermistor must have good thermal contact with the battery cells for proper protection.

4. **Header Connections**: All power, ground, I2C, and thermal sensing signals are routed to a single main header connector.

## Getting Started

1. Review the [SCHEMATIC.md](docs/SCHEMATIC.md) document for circuit design
2. Check the [BOM.md](docs/BOM.md) for required components
3. Refer to [VARIANT-1.md](docs/VARIANT-1.md) for assembly instructions
4. Use [PINOUT.md](docs/PINOUT.md) for header connections

## Safety Warnings

⚠️ **Important Safety Information**:
- Always observe proper polarity when connecting power
- Do not exceed maximum cell voltage (3.65V per cell)
- Do not discharge below minimum cell voltage (2.5V per cell)
- Ensure temperature sensors are properly installed
- Use appropriate wire gauge for current requirements
- Follow all battery safety guidelines

## License

[Specify license here]

## Contributing

[Specify contribution guidelines here]

## Contact

[Specify contact information here]
