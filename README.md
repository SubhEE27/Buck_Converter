# LMR51450 Based Buck Converter (10–35 V → 7.6 V @ 4 A)

This project implements a **DC-DC Buck Converter** using the **Texas Instruments LMR51450** regulator IC.  
The design converts an input range of **10 V to 35 V** into a regulated **7.6 V output** at up to **4 A continuous current**.

The schematic, PCB layout, and BOM are included, designed in **KiCad**.

---

## 📐 Design Specifications
- Input Voltage Range: 10 – 35 V  
- Output Voltage: 7.6 V  
- Max Output Current: 4 A  
- Switching Frequency: ~500 kHz  
- Capacitor Type: X7R dielectric (temperature-stable, low ESR)  

---

## 🔧 Key Component Choices

- **Feedback Network**  
  - Output voltage set using divider resistors: ~90 kΩ (top), 10 kΩ (bottom).  

- **Switching Frequency**  
  - RT resistor: ~402 kΩ, corresponding to ~500 kHz operation.  

- **Inductor**  
  - Value: 4.7 µH  
  - Rated current: ≥ 7 A saturation, low DCR (<20 mΩ).  

- **Output Capacitor (COUT)**  
  - Requirement: ≥ 25 µF effective capacitance.  
  - Chosen: 2 × 22 µF, 16 V X7R ceramics → ~40 µF effective.  

- **Input Capacitor (CIN)**  
  - Requirement: rated ≥ 2 × VINmax (≥ 50 V).  
  - Chosen: 2 × 4.7 µF, 50 V X7R ceramics, plus 0.1 µF ceramic for high-frequency filtering.  

- **Bootstrap Capacitor (CBOOT)**  
  - 0.1 µF, 16 V X7R ceramic.  

- **Feedforward Capacitor (CFF)**  
  - ~15 pF, improves transient response and loop stability.  

---

## 🧾 BOM (Major Components)

| Reference | Value / Part         | Notes                               |
|-----------|----------------------|-------------------------------------|
| U1        | LMR51450             | Buck regulator IC                   |
| L1        | 4.7 µH, 7 A sat.     | Shielded power inductor             |
| CIN       | 2 × 4.7 µF, 50 V X7R | Input decoupling (low ESR)          |
| COUT      | 2 × 22 µF, 16 V X7R  | Output filter cap                   |
| CBOOT     | 0.1 µF, 16 V X7R     | Bootstrap capacitor                 |
| RFBT      | ~90 kΩ               | Feedback resistor (top)             |
| RFBB      | 10 kΩ                | Feedback resistor (bottom)          |
| CFF       | 15 pF                | Feedforward capacitor               |
| RT        | 402 kΩ               | Sets switching frequency            |

---

## 🖇️ Layout Guidelines
- Use a **solid ground plane** (bottom layer for 2-layer PCB).  
- Place **input capacitors (CIN)** as close as possible to VIN–PGND pins with direct vias.  
- Keep **SW node copper small** to reduce EMI.  
- Place **output capacitors (COUT)** close to the inductor and PGND return.  
- Stitch PGND and AGND together at a single point to minimize noise.  

---

## 📂 Repository Contents
- `/schematics/` → KiCad schematic files  
- `/pcb/` → PCB layout files  
- `/bom/` → Bill of Materials  
- `README.md` → This document  

---

## 📌 Notes
- All capacitors use **X7R dielectric** for thermal stability and low ESR.  
- Input capacitors are rated at least **2× the maximum VIN** for reliability.  
- Design optimized for **low ripple**, **high efficiency**, and **fast transient response**.
