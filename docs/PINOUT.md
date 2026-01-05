# Header Pinout - Simple2S2C Battery Pack

## Main Header (J1)

This header consolidates all external connections for the battery pack system.

### Pinout Table

| Pin | Signal Name | Direction | Description | Notes |
|-----|-------------|-----------|-------------|-------|
| 1 | GND | - | Ground / Battery Negative | Common ground for all signals |
| 2 | VBAT+ | Output | Battery Pack Positive Output | Protected battery output |
| 3 | VIN+ | Input | Charging Input Positive | Input for battery charging |
| 4 | VIN- / GND | Input | Charging Input Ground | Shared with pin 1 |
| 5 | SCL | Bidir | I2C Serial Clock | Shared I2C bus |
| 6 | SDA | Bidir | I2C Serial Data | Shared I2C bus |
| 7 | TMP117_VDD | Input | TMP117 External Power Supply | NOT from battery pack |
| 8 | TMP117_GND | - | TMP117 Ground | Connected to common ground |
| 9 | THERMAL_SENSE_1 | Input | Thermal Pad Sense Pin 1 | From thermal pad |
| 10 | THERMAL_SENSE_2 | Input | Thermal Pad Sense Pin 2 | From thermal pad (optional) |

## Signal Descriptions

### Power Signals
- **GND**: Common ground reference for all circuits
- **VBAT+**: Protected battery output, suitable for load connection
- **VIN+/VIN-**: Charging input, protected by BQ29209

### I2C Bus
- **SCL/SDA**: Shared I2C communication bus
  - Connected to BQ29209 (if I2C monitoring is supported)
  - Connected to TMP117 for temperature readout
  - Requires external pull-up resistors (typically 4.7kΩ)

### TMP117 Power
- **TMP117_VDD**: External power supply for TMP117 (typically 1.7V to 5.5V)
- **TMP117_GND**: Ground return for TMP117 (common with main ground)
- **Note**: TMP117 is intentionally powered separately from the battery pack

### Thermal Pad Connections
- **THERMAL_SENSE_1/2**: Connection points for thermal pad sensing
- These may be analog voltage outputs or digital signals depending on thermal pad design

## I2C Device Addresses

| Device | Default I2C Address | Notes |
|--------|-------------------|-------|
| BQ29209 | N/A | BQ29209 may not have I2C (depends on specific variant) |
| TMP117 | 0x48 (default) | Configurable via ADD0 pin |

## Electrical Specifications

- **VBAT+ Output**: 5.0V to 7.3V nominal (2S LiFePO4)
- **VIN+ Input**: 7.0V to 7.6V (for 2S LiFePO4 charging)
- **I2C Bus**: 3.3V or 5V logic levels (ensure compatibility)
- **TMP117_VDD**: 1.7V to 5.5V
- **Maximum Current**: TBD based on BQ29209 and MOSFET ratings

## Connection Guidelines

1. Ensure proper polarity for power connections
2. Use appropriate wire gauge for current requirements
3. Keep I2C traces short and use pull-up resistors
4. Provide clean power supply for TMP117
5. Ensure thermal pad has good thermal contact with battery cells
