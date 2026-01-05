# Variant-1 Assembly Documentation

## Overview
Variant-1 represents the baseline configuration of the Simple2S2C battery pack system. This variant includes all core components required for a protected 2S LiFePO4 battery pack with dual temperature monitoring.

## Assembly Components

### Main PCB Assembly
1. **BQ29209 Battery Protection IC (U1)**
   - Provides overvoltage, undervoltage, and overcurrent protection
   - Monitors NTC thermistor for temperature protection
   - Controls charge/discharge MOSFETs

2. **Charge/Discharge MOSFETs (Q1, Q2)**
   - Two N-channel MOSFETs for charge and discharge path control
   - Controlled by BQ29209
   - Sized for application current requirements

3. **NTC Thermistor (RT1)**
   - 10kΩ @ 25°C NTC thermistor
   - Mounted in close thermal contact with battery cells
   - Connected to BQ29209 TS pin for critical temperature monitoring

4. **TMP117 Temperature Sensor (U2)**
   - High-accuracy I2C digital temperature sensor
   - Externally powered (NOT from battery pack)
   - Provides precision temperature monitoring independent of battery state

5. **Passive Components**
   - Resistors (R1-R4): I2C pull-ups, voltage dividers, bias resistors
   - Capacitors (C1-C4): Bypass and filter capacitors
   - Values per component datasheets

6. **Main Header Connector (J1)**
   - 10-pin header (minimum)
   - Provides access to:
     - Ground
     - Battery power output
     - Charging power input
     - I2C bus (SCL, SDA)
     - TMP117 external power
     - Thermal pad connections

### Battery Cell Assembly
1. **Two Calb DTP803450 LiFePO4 Cells**
   - Connected in series (2S configuration)
   - 6.4V nominal, 7.3V maximum
   - Mounted with appropriate mechanical support

2. **Battery Interconnects**
   - Series connection between Cell 1 and Cell 2
   - Connections to BQ29209 monitoring points
   - Power path through MOSFETs to output

### Thermal Management Assembly
1. **Thermal Pad (TP1)**
   - Option A: Thin FR4 or aluminum-backed PCB
   - Option B: Silicone thermal pad
   - Positioned for thermal contact with battery cells
   - Includes temperature sensing capability

2. **Thermal Pad Header**
   - Separate pins for thermal sense signals
   - Connected to main header (J1)
   - Allows external monitoring of thermal pad

## Assembly Configuration

### Power Architecture
```
Battery Cells (2S) → BQ29209 → MOSFETs → Header Output
                      ↓
                    NTC Sensor
```

### I2C Bus Architecture
```
Header I2C Pins (SCL/SDA)
    ├── TMP117 (externally powered)
    └── (Future expansion)
```

### Temperature Monitoring
1. **Primary (Critical)**: NTC thermistor → BQ29209
   - Used for battery protection decisions
   - Triggers charge/discharge cutoff on over/under temperature

2. **Secondary (Monitoring)**: TMP117 → I2C → External controller
   - High-precision temperature logging
   - Independent of battery state
   - Externally powered

3. **Tertiary (Optional)**: Thermal pad sensors
   - Additional thermal monitoring points
   - Available via header pins

## Key Features of Variant-1

### Protection Features
- ✓ Overvoltage protection per cell
- ✓ Undervoltage protection per cell
- ✓ Overcurrent protection (charge and discharge)
- ✓ Short circuit protection
- ✓ Over-temperature protection (via NTC)
- ✓ Under-temperature protection (via NTC)

### Monitoring Features
- ✓ Cell voltage monitoring (via BQ29209)
- ✓ Critical temperature monitoring (via NTC → BQ29209)
- ✓ Precision temperature monitoring (via TMP117 → I2C)
- ✓ Thermal pad sensing (via header pins)

### Interface Features
- ✓ Protected battery output
- ✓ Charging input
- ✓ I2C communication bus
- ✓ External power input for TMP117
- ✓ Thermal pad interface

## Assembly Notes

### Critical Requirements
1. **TMP117 Power**: Must be supplied externally, NOT from battery pack
2. **NTC Placement**: Must have good thermal contact with battery cells
3. **Thermal Pad**: Must be properly positioned for heat transfer
4. **Polarity**: Verify all power connections before assembly
5. **I2C Pull-ups**: Required on SCL and SDA lines (typically 4.7kΩ)

### Recommended Assembly Sequence
1. Populate and solder PCB components (U1, U2, Q1, Q2, passives)
2. Install main header connector (J1)
3. Mount battery cells with mechanical support
4. Install NTC thermistor in thermal contact with cells
5. Position and secure thermal pad
6. Connect thermal pad to header pins
7. Make battery cell interconnections
8. Connect battery cells to PCB
9. Final inspection and testing

### Testing and Validation
Before deployment, verify:
- [ ] Cell voltages are balanced and within spec
- [ ] BQ29209 protection thresholds are correctly configured
- [ ] NTC thermistor is reading correct temperature
- [ ] TMP117 communicates correctly on I2C bus (with external power)
- [ ] Charge/discharge MOSFETs operate correctly
- [ ] All header pins have proper connectivity
- [ ] Polarity is correct on all power connections
- [ ] Thermal pad is properly positioned

## Future Variants

### Potential Variant-2 Enhancements
- Additional temperature sensors
- Battery heater integration
- Alternative thermal pad designs
- Different cell configurations
- Enhanced I2C monitoring features
- Additional protection features

## Revision History

| Version | Date | Description |
|---------|------|-------------|
| Variant-1 | 2026-01-05 | Initial baseline configuration |
