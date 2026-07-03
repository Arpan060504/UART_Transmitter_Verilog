# UART Transmitter in Verilog HDL

Short project description...

---

## Features

- Moore FSM based UART Transmitter
- 8-bit parallel to serial transmission
- LSB-first transmission
- Start bit generation
- Stop bit generation
- Baud counter
- Busy signal
- Reset support
- RTL verification

---

## FSM States

- IDLE
- START
- SEND_BIT
- STOP

(Brief explanation of each.)

---

## Inputs

| Signal | Description |
|---------|-------------|
| clk | System clock |
| reset | Active-high reset |
| tx_start | Starts transmission |
| tx_data | 8-bit parallel input |

---

## Outputs

| Signal | Description |
|---------|-------------|
| tx | UART serial output |
| busy | Indicates transmitter is busy |

---

## Internal Registers

- Shift Register
- Bit Counter
- Baud Counter
- State Register

---

## Project Structure
