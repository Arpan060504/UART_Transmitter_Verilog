# UART Transmitter in Verilog HDL

A Finite State Machine (FSM) based UART (Universal Asynchronous Receiver Transmitter) Transmitter implemented in Verilog HDL. This project performs asynchronous serial communication by converting 8-bit parallel data into a serial data stream following the UART protocol. The design includes baud rate timing, start/stop bit generation, shift-register based serialization, busy indication, and comprehensive RTL verification using a Verilog testbench.

---

## Features

- Moore FSM-based UART Transmitter
- 8-bit Parallel-to-Serial Data Transmission
- LSB-First Transmission
- Start Bit Generation
- Stop Bit Generation
- Baud Rate Timing Control using Baud Counter
- Busy Signal Indication
- Active-High Reset
- Fully Verified using Testbench
- GTKWave Compatible Simulation

---

## UART Frame Format

```
Idle  Start   D0  D1  D2  D3  D4  D5  D6  D7  Stop
  1      0     LSB -----------------------> MSB   1
```

Example:

For

```
tx_data = 8'hA5
```

Binary:

```
10100101
```

UART transmits

```
0 | 1 0 1 0 0 1 0 1 | 1
↑   LSB First        ↑
Start               Stop
```

---

## FSM States

| State | Description |
|--------|-------------|
| **IDLE** | Waits for a transmission request while TX remains HIGH. |
| **START** | Loads input data into the shift register and transmits the START bit (LOW). |
| **SEND_BIT** | Serially transmits one data bit every baud interval while shifting the register. |
| **STOP** | Transmits the STOP bit (HIGH) and returns to the IDLE state. |

---

## Inputs

| Signal | Width | Description |
|---------|------:|-------------|
| clk | 1 | System Clock |
| reset | 1 | Active-High Reset |
| tx_start | 1 | Starts UART Transmission |
| tx_data | 8 | Parallel Data Input |

---

## Outputs

| Signal | Width | Description |
|---------|------:|-------------|
| tx | 1 | UART Serial Output |
| busy | 1 | Indicates Transmitter is Busy |

---

## Internal Registers

- State Register
- Next-State Logic
- 8-bit Shift Register
- 3-bit Bit Counter
- Baud Counter

---

## Design Flow

```
          +-------------+
          |   IDLE      |
          +-------------+
                 |
          tx_start = 1
                 |
                 v
          +-------------+
          |   START     |
          +-------------+
                 |
                 v
          +-------------+
          | SEND_BIT    |
          +-------------+
                 |
      8 Bits Transmitted
                 |
                 v
          +-------------+
          |    STOP     |
          +-------------+
                 |
                 v
          +-------------+
          |    IDLE     |
          +-------------+
```

---

## Project Structure

```
UART_Transmitter_Verilog
│
├── rtl
│   └── uart_tx.v
│
├── tb
│   └── uart_tx_tb.v
│
├── docs
│   └── uart_fsm.png
│
├── waveforms
│   └── uart_waveform.png
│
└── README.md
```

---

## Simulation

### Compile

```bash
iverilog -Wall -o uart_sim rtl/uart_tx.v tb/uart_tx_tb.v
```

### Run

```bash
vvp uart_sim
```

### Open Waveform

```bash
gtkwave uart_test.vcd
```

---

## Test Cases Verified

- ✅ Reset Operation
- ✅ Transmission of `8'hA5`
- ✅ Transmission of `8'h00`
- ✅ Transmission of `8'hFF`
- ✅ Transmission of `8'hAB`
- ✅ Busy Signal Verification
- ✅ Multiple Consecutive Transmissions
- ✅ Ignoring New Requests While Busy

---

## Simulation Waveform

> Add a GTKWave screenshot here.

```
waveforms/uart_waveform.png
```

---

## Future Improvements

- UART Receiver
- UART Transceiver
- Configurable Baud Rate Generator
- Even/Odd Parity Support
- Configurable Stop Bits
- FIFO Buffer
- Interrupt Support

---

## Tools Used

- Verilog HDL
- Icarus Verilog
- GTKWave
- Visual Studio Code
- Git & GitHub

---

## Learning Outcomes

This project demonstrates:

- Finite State Machine (FSM) Design
- RTL Design using Verilog HDL
- Shift Register Implementation
- Parallel-to-Serial Data Conversion
- UART Communication Protocol
- Sequential Logic Design
- RTL Simulation and Verification
- Digital System Debugging using GTKWave

---

## Author

**Arpan Roy**

Electrical Engineering Undergraduate  
National Institute of Technology Durgapur

GitHub: https://github.com/Arpan060504
