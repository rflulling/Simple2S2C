# Component Specifications - Simple2S2C Battery Pack

## Battery Cells

### Calb DTP803450 LiFePO4 Cells

**Electrical Characteristics:**
- Chemistry: Lithium Iron Phosphate (LiFePO4)
- Nominal Voltage: 3.2V
- Charge Voltage: 3.65V (max)
- Discharge Cut-off: 2.5V (min)
- Typical Capacity: ~800-1000mAh (varies by specific model)
- Form Factor: Pouch cell

**Configuration:**
- 2S (Series): 6.4V nominal, 7.3V max charge

**Safety Features:**
- Inherently safer chemistry than Li-ion
- Lower risk of thermal runaway
- Longer cycle life

## Battery Protection IC

### BQ29209 - Battery Protection Controller

**Features:**
- 2-series cell protection for Li-ion and LiFePO4 chemistries
- Overvoltage protection (OVP)
- Undervoltage protection (UVP)
- Overcurrent protection (OCP)
- Short circuit protection (SCP)
- Temperature monitoring via external NTC

**Key Specifications:**
- Supply Voltage: 4V to 26V
- Quiescent Current: Low µA range
- Voltage Detection Accuracy: High precision
- Temperature Sensing: External NTC thermistor input
- Control: External N-channel MOSFETs for charge/discharge control

**Pin Functions:**
- VC1, VC2: Cell voltage monitoring inputs
- VSS: Ground
- V+: Supply voltage (from battery pack)
- TS: Temperature sense (NTC input)
- CHG: Charge FET control output
- DSG: Discharge FET control output
- (Additional pins per datasheet)

## Temperature Sensors

### NTC Thermistor (for BQ29209)

**Specifications:**
- Type: Negative Temperature Coefficient
- Resistance: 10kΩ @ 25°C (typical)
- Beta Value: 3950K (typical)
- Tolerance: ±1% to ±5%
- Operating Range: -40°C to +125°C

**Application:**
- Mounted in thermal contact with battery cells
- Connected to BQ29209 TS pin with appropriate bias resistor
- Provides over-temperature and under-temperature protection

### TMP117 - High-Accuracy Digital Temperature Sensor

**Features:**
- High accuracy: ±0.1°C (typ) from -20°C to +50°C
- High accuracy: ±0.2°C (max) from -40°C to +100°C
- Resolution: 16-bit (0.0078°C/LSB)
- Interface: I2C (up to 400kHz)
- Supply Voltage: 1.7V to 5.5V
- Low Power: <150µA active, <250nA shutdown

**Pin Configuration:**
- VDD: Power supply (external, NOT from battery)
- GND: Ground
- SCL: I2C clock
- SDA: I2C data
- ADD0: Address select pin (optional)

**I2C Address:**
- Default: 0x48
- Configurable: 0x48, 0x49, 0x4A, 0x4B (via ADD0 pin)

**Application:**
- Precision temperature monitoring
- Externally powered for independent operation
- Can continue monitoring even when battery is disconnected
- Useful for ambient and system temperature tracking

## Thermal Pad

### Thermal Interface Options

**Option 1: Thin PCB**
- Material: FR4 or aluminum-backed PCB
- Thickness: 0.4mm to 1.0mm
- Features: Copper traces for thermal distribution
- Sensing: Thermistor or temperature sensor mounted on PCB

**Option 2: Silicone Thermal Pad**
- Material: Thermally conductive silicone
- Thickness: 0.5mm to 2.0mm
- Thermal Conductivity: 3-6 W/mK
- Features: Flexible, compressible
- Sensing: Embedded sensor or surface-mount sensor

**Header Interface:**
- Separate pins for thermal sense signals
- Ground reference pin
- Optional power if active sensors used

## Power MOSFETs

### Charge/Discharge Control FETs

**Requirements:**
- Type: N-channel MOSFETs
- VDS Rating: ≥ 20V (for safety margin)
- RDS(on): Low resistance for efficiency (< 10mΩ typical)
- ID Rating: Based on max charge/discharge current
- VGS(th): Compatible with BQ29209 gate drive voltage
- Package: TO-252 (DPAK), SO-8, or similar

**Typical Selections:**
- Si4946BEY (Vishay)
- IRFR3710 (Infineon)
- Or equivalent based on current requirements

## Passive Components

### Resistors
- I2C Pull-ups: 4.7kΩ (typical)
- Voltage Dividers: Per BQ29209 datasheet requirements
- NTC Bias: Per BQ29209 datasheet requirements
- Gate Pull-downs: 100kΩ to 1MΩ

### Capacitors
- Bypass Caps: 0.1µF to 1µF ceramic
- Bulk Caps: 10µF to 100µF (if needed)
- Filter Caps: Per BQ29209 recommendations
- TMP117 Bypass: 0.1µF ceramic

## Connector

### Main Header
- Type: Through-hole or surface-mount header
- Pitch: 2.54mm (0.1") standard or 2.0mm compact
- Pins: 10-pin (minimum for described functionality)
- Current Rating: Sufficient for max battery current
- Options: Molex, JST, or standard pin header
