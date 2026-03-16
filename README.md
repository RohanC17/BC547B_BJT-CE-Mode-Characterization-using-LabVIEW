# BJT Characterization System (Common Emitter Mode)

This repository contains an automated measurement and instrumentation system developed to characterize a **Small-Signal NPN BJT (BC547B)** in Common-Emitter (CE) configuration. 

The system utilizes a **USB Data Acquisition (DAQ)** device and **LabVIEW** to perform automated voltage sweeps, allowing for the precise mapping of a transistor's operating regions: Cutoff, Forward-Active, and Saturation.

## 📋 Project Overview
The core objective is to generate the $I_C - V_{CE}$ relationship by modulating base current ($I_B$) and sweeping collector-emitter voltage ($V_{CE}$). This provides a practical understanding of semiconductor physics, including the **Early Effect** and **Current Gain ($\beta$)**.

### Key Features
* **Automated Two-Tier Sweep**: A nested loop structure where the outer loop steps through base bias ($V_B$) and the inner loop sweeps collector voltage ($V_C$).
* **Precision Signal Conditioning**: Uses an **LM324 Op-Amp** for voltage buffering and scaling ($4.03\times$ gain stage).
* **Thermal Monitoring**: Integrated **LM335 temperature sensor** to correlate thermal drift with transistor behavior (variation in $V_{BE}$ and $\beta$).
* **Real-Time Data Processing**: Dynamic calculation of $I_B$ and $I_C$ using Ohm’s Law across precision sense resistors ($2.35\text{ k}\Omega$ base resistance and $15\text{ k}\Omega$ collector resistance).

## 🛠️ Hardware Schematic
The system is built upon a custom measurement testbench featuring:
* **Transistor**: BC547B (NPN).
* **Buffering**: LM324N Operational Amplifiers to ensure high input impedance and stable biasing.
* **Sensors**: LM335 for absolute temperature measurement ($10\text{ mV/K}$ scaling).
* **DAQ Interfacing**:
    * **A00/A01**: Analog Outputs for base and collector control.
    * **AI0/AI1/AI2/AI4**: Analog Inputs for monitoring $V_{BE}$, $V_{CE}$, and Temperature.


## 💻 LabVIEW Implementation
The Virtual Instrument (VI) architecture is designed for synchronization and accuracy:
1. **Outer Loop (5 Steps)**: Sets the base bias voltage levels.
2. **Inner Loop (16 Steps)**: Sweeps the collector-emitter voltage.
3. **Data Bundling**: Clusters $(I_B, V_{CE}, I_C)$ tuples for multi-plot XY Graph visualization.
4. **Temperature Conversion**: Implements the formula $T(^\circ\text{C}) = (100 \times V_{LM335}) - 273.15$ for real-time Celsius display.

## 📈 Technical Specifications & Physics
* **Current Gain Relationship**: $I_C \approx \beta \cdot I_B$.
* **Early Effect Modeling**: $I_C(V_{CE}) \approx I_{C0} \cdot (1 + \frac{V_{CE}}{V_A})$, where $V_A$ is the Early Voltage.
* **Saturation Voltage**: Typically observed between $0.05\text{ V}$ and $0.3\text{ V}$.

## 🚀 How to Run
1. **Hardware**: Connect the BC547B and signal conditioning circuit to your USB DAQ.
2. **Setup**: Open the main LabVIEW VI.
3. **Execution**: Run the VI to begin the automated sweep. 
4. **Analysis**: View the family of curves on the "IV Characterization" tab and individual parameter readings on the "Readings" tab.

---
*Developed by Rohan Channakeshavaiah at Hochschule Bremen (City University of Applied Sciences).*
