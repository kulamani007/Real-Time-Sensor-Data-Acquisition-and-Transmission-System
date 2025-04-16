# FPGA-based Ultrasonic Sensor Data Acquisition System

This project implements a simple **ultrasonic distance measurement system** using an **VSDSquadron mini FPGA board** and **HC-SR04 ultrasonic sensor**. The design is implemented in Verilog HDL and the measured distance is transmitted over UART, which can be monitored through a serial terminal like `screen` or `minicom` on a Linux machine.

---

## 📷 Overview

- **Sensor**: HC-SR04 Ultrasonic Sensor
- **FPGA**: VSDSquadron mini FPGA (TQ144 package)
- **Interface**: UART Serial at 9600 baud rate
- **Tools Used**:
  - Yosys (for synthesis)
  - nextpnr (for placement and routing)
  - IceStorm (for bitstream generation)
  - IceProg (for flashing)
  - Screen/Minicom (for UART monitor)

---

## 🔁 Working Principle

1. FPGA sends a **trigger pulse** to the HC-SR04.
2. The sensor sends an **ultrasonic pulse** and raises its echo pin when the pulse bounces back.
3. The FPGA captures the **duration of the echo signal**.
4. Using this duration, it calculates the **distance** and sends it over UART.

---

## 📦 Pin Connections

| Signal      | FPGA Pin (DPIO) | Description           |
|-------------|------------------|-----------------------|
| `clk`       | 20               | 12 MHz external clock |
| `trig`      | 4                | Trigger output to HC-SR04 |
| `echo`      | 3                | Echo input from HC-SR04   |
| `tx`        | 14               | UART TX for serial communication |
| `rx`        |15                | UART RX for serial communication |

**Note:** All pin numbers follow the **DPIO header labeling** from the FPGA board. Refer to your board's datasheet for exact mapping.

---

## 🔌 Circuit Diagram

```
            +-----------------------+
            |   VSDSquadron FPGA    |
            |                       |
            |   20 ---> clk         |
            |   4  ---> trig        |
            |   3  <--- echo        |
            |   14 ---> tx (UART)   |
            +-----------------------+
                       |
                       |
                +-------------+
                |  HC-SR04    |
                |             |
                |  VCC -- +5V |
                |  GND -- GND |
                |  TRIG<- trig|
                |  ECHO-> echo|
                +-------------+
```

---

## 🛠️ How to Run the Project

1. **Clone the project and navigate to the folder:**

```bash
git clone <your_project_repo>
cd <project_folder>
```

2. **Build the Verilog source:**

```bash
make
```

3. **Flash the bitstream to the board:**

```bash
iceprog top.bin
```

4. **Monitor UART Output:**

```bash
screen /dev/ttyUSB0 9600
```

(Or use `minicom` as an alternative.)

---

## 📏 Sample UART Output

```
Distance: 12 cm
Distance: 13 cm
Distance: 15 cm
...
```



https://github.com/user-attachments/assets/bd542388-58fd-40b1-a841-83fd9c5218fc



---

## ✅ Status

✔️ Verilog modules implemented  
✔️ UART transmission working  
✔️ Sensor input correctly received  


---

## 🔚 Conclusion

This project demonstrates a simple yet effective method of reading sensor data directly using FPGA logic and transmitting data via UART. It’s a great beginner-friendly integration of sensors with HDL design.

---
