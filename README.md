# IoT Lab — Continuous Assessment Tasks (CATs)

This repository holds the firmware source code, hardware schematics, circuit diagrams, and compiled deliverables for all IoT Lab continuous‑assessment experiments.

**Student Register No.:** `25011102043`

---

## Repository Structure

```
repo/
├── .gitignore
├── README.md
├── 8051/
│   ├── CAT2/   # Bare-Metal LED Blink
│   ├── CAT3/   # Timer-Based LED Pattern & Button Controller
│   ├── CAT4/   # Matrix Keypad, 7-Segment Display & LED Interface
│   ├── CAT5/   # Hardware Timer PWM, Signal Generation & Stepper Motor
│   ├── CAT6/   # UART Serial Communication (TX & Echo)
│   └── CAT7/   # 16x2 LCD Driver & Dynamic Character Movement
└── STM32/
    ├── CAT8/   # GPIO Bring-Up & Switch-Controlled LED
    ├── CAT9/   # Hardware Timers & Serial Control
    ├── CAT10/  # STM32-ESP8266 Wi-Fi Modem Interface
    ├── CAT11/  # USART Telemetry & Peripheral Drivers
    ├── CAT12/  # BME280 Sensor Interfacing via I²C
    ├── CAT13/  # MQTT Cloud Telemetry via ESP8266
    ├── CAT14/  # Multi-Sensor Telemetry & Edge Gateway
    └── CAT15/  # BME280 Weather Station & MQTT Dashboard
```

---

## Index

### 8051 Microcontroller (Atmel AT89S52)

All 8051 experiments are written in bare‑metal Embedded C with direct register‑level access — no third‑party libraries or RTOS:

| Evaluation | Topic / Experiment | Description | Deliverables |
|---|---|---|---|
| **CAT2** | Hardware Bring-Up & LED Blink | Direct GPIO register write to toggle an LED at ~1 Hz using a software delay loop. | `prog1.c`, `STARTUP.A51`, `.hex` |
| **CAT3** | Timer & Button State Controller | Multi‑mode state machine (Running LED, Binary Counter, Alternating, Flashing) with hardware debouncing via timer interrupts. | `prog1.c`, `STARTUP.A51`, `.hex` |
| **CAT4** | Matrix Keypad, 7-Segment & LEDs | 4×4 keypad row/column scan driving a 7‑segment numerical display with simultaneous multi‑mode LED actuation. | `prog1.c`, `STARTUP.A51`, `.hex` |
| **CAT5** | PWM, Waveforms & Stepper Motor | Hardware timer‑driven non‑blocking LED fading (PWM), variable‑frequency waveform generation, and stepper‑motor coil sequencing. | `TASK5A/`, `TASK5B/`, `.c`, `STARTUP.A51`, `.hex` |
| **CAT6** | UART Serial Communications | Hardware UART string transmission at 9600 baud and full‑duplex interactive echo terminal via `TASK6A/`. | `TASK6A/`, `.c`, `STARTUP.A51`, `.hex` |
| **CAT7** | 16×2 LCD Driver & Keypad Movement | HD44780 4‑bit LCD driver with string/number formatting and keypad‑controlled cursor movement across tasks A–C. | `TASK7A/`, `TASK7B/`, `TASK7C/`, `.c`, `STARTUP.A51`, `.hex` |

---

### STM32 Microcontroller (STM32F401RE Nucleo)

All STM32 projects are configured via STM32CubeMX and built with ARM Keil MDK (using STM32 HAL & CMSIS drivers):

| Evaluation | Topic / Experiment | Target Hardware | Deliverables |
|---|---|---|---|
| **CAT8** | GPIO Bring-Up & Switch-Controlled LED | STM32F401RE (Nucleo) | GPIO input/output with push‑button debounce; short‑press and long‑press LED response across `TASK8A/`, `TASK8B/`, `TASK8C/`. |
| **CAT9** | Hardware Timers & Serial Control | STM32F401RE (Nucleo) | Hardware timer peripheral configuration; serial command parser controlling LED state via `TASK9A/`. |
| **CAT10** | ESP8266 Wi-Fi Modem Interface | STM32F401RE + ESP8266 | AT command interface over USART to the ESP8266 module across `TASK10A/`, `TASK10B/`, `TASK10C/`. |
| **CAT11** | USART Telemetry & Heartbeat | STM32F401RE (Nucleo) | USART2 at 115200 baud streaming periodic sensor heartbeat data via `TASK11A/`. |
| **CAT12** | BME280 Sensor Interfacing via I²C | STM32F401RE (Nucleo) | Bosch BME280 driver over I²C reading temperature, pressure & humidity across `TASK12A/`, `TASK12B/`, `TASK12C/`. |
| **CAT13** | MQTT Cloud Telemetry | STM32F401RE + ESP8266 | Custom ESP8266 AT command API publishing sensor data over MQTT to a cloud broker via `TASK13/`. |
| **CAT14** | Multi-Sensor Telemetry & Edge Gateway | STM32F401RE + ESP8266 | BME280 I²C sensor fused with ESP8266 MQTT telemetry forming an embedded edge‑gateway node via `TASK14/`. |
| **CAT15** | BME280 Weather Station & MQTT Dashboard | STM32F401RE + ESP8266 | End‑to‑end weather‑station pipeline: I²C sensor → UART → ESP8266 → MQTT broker → Node‑RED dashboard via `TASK15/`. |

---

## Build & Flash Guide

### 8051
1. Open the Keil uVision project (`.uvprojx`) inside the experiment folder.
2. Build the project (**F7** or Project → Build Target).
3. Connect a **USBasp** programmer to the AT89S52 board.
4. Flash the generated `.hex` via avrdude or Keil's Flash Download.
5. Reset the board and verify operation.

### STM32
1. Open the STM32CubeIDE project (`.ioc` file or `Core/` folder).
2. Build the firmware (Project → **Build All** or **F7**).
3. Connect the **ST‑Link V2** programmer.
4. Flash via the IDE (Run → **Debug**) or use ST‑Link Utility.
5. Reset the Nucleo board and verify the expected behaviour.

---

## Notes
- Each experiment folder contains a `README.md` with a circuit diagram, firmware overview, and task‑specific build notes.
- All circuit diagrams are stored as `circuit.png` within their respective category folder.
- The `.gitignore` excludes compiled object files, IDE caches, and binary artefacts not required for evaluation.
