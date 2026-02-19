# High-Speed Multi-Clock Image Streaming Architecture over UART

## Overview

This project implements a robust RTL-based image streaming architecture over UART, designed for reliable high-throughput data transfer between a PC and an FPGA.

The system supports 256×256 pixel image transmission at a 5 MHz baud rate and demonstrates advanced digital design concepts including clock domain crossing (CDC), hardware flow control, asynchronous FIFOs, and dual-port SRAM architecture.

---

## Top-Level Architecture

![Top Level Architecture](Doc/Top_level_uArch.png)

> Replace the image path above with your actual diagram location.

---

## Key Features

- Multi-clock domain architecture  
- Safe Clock Domain Crossing (CDC) implementation  
- Asynchronous FIFOs with Gray-coded pointers  
- Hardware flow control using RTS/CTS  
- Dual-port SRAM for RGB channel storage  
- 128-bit message framing protocol  
- Backpressure-aware RX/TX sequencers  
- Glitchless clock switching (PLL integration)

---

## Architecture Overview

### Data Path

1. **UART RX** receives serialized image data.
2. **Parser + Classifier** decodes messages and separates RGB channels.
3. **RX Sequencer** writes pixel data into asynchronous FIFOs.
4. **Dual-Port SRAM** stores RGB data (4 pixels per address).
5. **TX Sequencer** reads data, composes messages, and transmits via UART TX.

### Clock Domains

- `sys_clk` (100 MHz system clock)
- `pll_clk` (high-speed clock domain)
- UART clock (derived from baud generator)

CDC is handled using:
- Asynchronous FIFOs
- Pulse synchronizers
- Multi-stage synchronizers

---

## Performance

- Message size: 128 bits (16 bytes)
- Baud rate: 5 MHz
- RX full image time ≈ 0.58 s  
- TX full image time ≈ 2.3 s  

---

## Tools & Environment

- SystemVerilog RTL
- Xilinx Vivado
- QuestaSim
- Python GUI for image transmission

---

## Project Goals

This project demonstrates:

- Safe multi-domain RTL design
- Memory architecture planning
- Flow control and backpressure management
- High-speed serial data handling
- FPGA system-level integration

---

## Author

Meitar Shimoni  
Chip Design & Verification  
Google Reichman Tech School

