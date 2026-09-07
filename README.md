# Experiment 3: Create and Use Classes and Objects to Model APB Packet.

---

## Aim  
To design and verify an **APB (Advanced Peripheral Bus) packet model** using **SystemVerilog object-oriented programming concepts** such as classes and objects, and simulate it using **ModelSim 2020.1**.

---

## Apparatus Required  
- Computer with **Windows OS**  
- **Synopsys VCS** 
---

## Description about APB Packet Modeling  
The **Advanced Peripheral Bus (APB)** is part of the AMBA protocol family used for connecting low-bandwidth peripherals.  
In this experiment, we use **SystemVerilog OOP concepts** to model an APB packet.  

- **Classes and Objects** in SystemVerilog allow abstraction and modularity.  
- An APB packet generally contains:  
  - **Address**  
  - **Data**  
  - **Control signals** (Read/Write, Select, Enable, Ready)  
- Using OOP, packets can be **created, initialized, randomized, and reused**, simplifying testbench construction.  

---

## Features  
- Written in **SystemVerilog OOP style**  
- Defines an **APB Packet class** with properties (address, data, control signals)  
- Includes **methods** for packet initialization and display  
- Demonstrates **object creation and manipulation**  
- Simulated using **Synopsys VCS**  

---

## Procedure  

1. **Open Synopsys VCS**  
   - Launch Synopsys VCS from Mobaxterm.  

2. **Create a New Project**  
   - `File → New → Project`.  
   - Name it `APB_Packet_Project`.  

3. **Add SystemVerilog Files**  
   - Create a file `apb_packet.sv` → Define the APB Packet class.  
   - Create a file `apb_tb.sv` → Instantiate objects and test the class.  

4. **Compile the Files**  
   - Select both `.sv` files.  
   - Right-click → **Compile Selected**.  
   - Ensure no errors exist.  

5. **Start Simulation**  
   - `Simulate → Start Simulation`.  
   - Select the testbench module (`apb_tb`).  

6. **Add Signals and Run**  
   - Add relevant signals to the waveform.  
   - Run the simulation for required time.  

7. **Analyze Output**  
   - Observe the creation and display of APB packets.  
   - Verify correct modeling of properties and methods.  

---

## SystemVerilog Code   

### APB Packet Class (`apb_packet.sv`)  
```systemverilog
class apb_packet;

  // APB packet properties
  rand bit [31:0] address;
  rand bit [31:0] data;
  bit             write;
  bit             select;
  bit             enable;
  bit             ready;

  // Constructor
  function new(
    bit [31:0] addr = 32'h0000_0000,
    bit [31:0] dat  = 32'h0000_0000,
    bit         wr   = 0,
    bit         sel  = 1,
    bit         en   = 1,
    bit         rdy  = 1
  );
    address = addr;
    data    = dat;
    write   = wr;
    select  = sel;
    enable  = en;
    ready   = rdy;
  endfunction

  // Display method
  function void display();
    $display("----------------------------------------");
    $display("           APB PACKET");
    $display("----------------------------------------");
    $display("Address : %h", address);
    $display("Data    : %h", data);
    $display("Write   : %b", write);
    $display("Select  : %b", select);
    $display("Enable  : %b", enable);
    $display("Ready   : %b", ready);
    $display("----------------------------------------");
  endfunction

endclass
```

### APB Packet Class (`apb_tb.sv`) 
```systemverilog
module apb_tb;

  // Declare APB packet object
  apb_packet pkt;

  initial begin

    // Create object
    pkt = new();

    // Initialize packet values
    pkt.address = 32'h0000_1000;
    pkt.data    = 32'hABCD_1234;
    pkt.write   = 1;
    pkt.select  = 1;
    pkt.enable  = 1;
    pkt.ready   = 1;

    // Display packet
    pkt.display();

    $display("APB packet object created successfully.");
    $display("Simulation completed.");

    $finish;
  end

endmodule
```
---
### Simulation Output

<img width="1600" height="840" alt="image" src="https://github.com/user-attachments/assets/30121867-b360-4451-9c84-8f8cfc3081fa" />



---

### Result

The design and verification of an APB packet model using SystemVerilog classes and objects was successfully carried out in ModelSim 2020.1.
The experiment demonstrated how OOP concepts simplify modeling and reusability in SystemVerilog testbenches.
