# Bill of Materials (BOM) - Simple2S2C Battery Pack

## Variant-1 Assembly

| Ref | Qty | Manufacturer | Part Number | Description | Notes |
|-----|-----|--------------|-------------|-------------|-------|
| U1 | 1 | Texas Instruments | BQ29209 | 2-Series Cell Li-Ion Battery Protection IC | Primary battery management IC |
| CELL1, CELL2 | 2 | CALB | DTP803450 | LiFePO4 Battery Cell, 3.2V | Series configuration |
| RT1 | 1 | TBD | NTC Thermistor | NTC Temperature Sensor, 10kΩ @ 25°C | For BQ29209 temperature monitoring |
| U2 | 1 | Texas Instruments | TMP117 | High-Accuracy Digital Temperature Sensor | I2C interface, externally powered |
| J1 | 1 | TBD | Header Connector | Main header for power, ground, and I2C | Pin count TBD based on final design |
| TP1 | 1 | TBD | Thermal Pad | Thin PCB or silicone thermal pad | With header pins for thermal sensing |
| Q1, Q2 | 2 | TBD | N-Channel MOSFET | Charge/Discharge control FETs | Selected based on BQ29209 requirements |
| R1-R4 | 4 | TBD | Resistor | Pull-up resistors for I2C, voltage dividers | Values per BQ29209 datasheet |
| C1-C4 | 4 | TBD | Capacitor | Bypass and filtering capacitors | Values per BQ29209 and TMP117 datasheets |

## Additional Components (TBD)
- Battery holders or cell mounting hardware
- PCB
- Wire harnesses
- Insulation materials
- Thermal interface material

## Notes
1. The TMP117 is NOT powered by the battery pack - external power required
2. All I2C devices (BQ29209 if capable, TMP117) share the same I2C bus on the header
3. Thermal pad includes separate header pins for thermal sensing
4. Component values (resistors, capacitors) to be determined from IC datasheets
5. MOSFET selection depends on maximum charge/discharge current requirements
