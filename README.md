# SPI Protocol Verification (SystemVerilog)

# Overview
This project implements and verifies a **basic SPI (Serial Peripheral Interface) protocol** using SystemVerilog.  
It includes:
- **SPI Master** (sends 12-bit data, LSB first)
- **SPI Slave** (receives and outputs data)
- **UVM-like Verification Environment** (Generator, Driver, Monitor, Scoreboard)

The goal is to test correct data transfer between master and slave using a **self-checking testbench**.
#  Features

### **Master**
- Generates `sclk` from `clk`
- Sends 12-bit `din` data when `newd=1`
- Sends **LSB first**
- Controls `cs` and `mosi`

### **Slave**
- Waits for `cs` low to start data reception
- Shifts in 12 bits from `mosi`
- Asserts `done` when full data is received
- Option to output `0` when `cs` is high to avoid garbage

### **Testbench Environment**
- **Generator**: Creates random 12-bit transactions
- **Driver**: Sends data to DUT (via interface)
- **Monitor**: Observes DUT outputs
- **Scoreboard**: Compares sent vs. received data
- **Mailbox/Event synchronization** for parallel processes

---

# Simulation Flow

1. **Reset Phase**  
   Driver applies reset to DUT.

2. **Data Generation**  
   Generator produces random `din` values for `count` iterations.

3. **Transmission**  
   Master sends data → Slave receives → `done` asserted.

4. **Monitoring & Checking**  
   Monitor captures output `dout`, Scoreboard compares with input.

5. **Result**  
   Displays **"DATA MATCHED"** or **"DATA MISMATCHED"** in console.



