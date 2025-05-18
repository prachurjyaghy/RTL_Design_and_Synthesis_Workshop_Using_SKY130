# DAY 1: Introduction to Verilog RTL design and Synthesis

## D1SK1 - Introduction to open-source simulator iverilog

### L1 - Introduction to iverilog design test bench
#### Simulator

### Introduction to Yosys
![image](https://github.com/user-attachments/assets/2d8ee06c-4c66-4986-a313-69666477a884)
### Verify synthesis
![image](https://github.com/user-attachments/assets/6d9e87a1-bbe2-41ea-824d-d37f224bd348)
  1. Stimulus to be same as output observed during TRL simulation
  2. The set of Promiary inputs / primary outputs will remain same between RTL design and Sythesiszed netlist. So same Test Bench can be used for RTL Test Bench

### Logic Synthesis
#### RTL Synthesis
![image](https://github.com/user-attachments/assets/f43d8723-5f18-4dc0-8cd2-8d6daee64468)
  1. RTL to Gate level translation
  2. Design conversion into gates and connections between gates
![image](https://github.com/user-attachments/assets/44498a7b-22f8-4b8d-94ea-daf1e9ab71bf)
  ##### .lib
    1. Collection of logical modules
    2. Includes basic logic gates with different flavours of same gate
    3. Ex: NAND and NOR unversal logic gates can be used to implement boolean logics
    4. Why Flavours required: Combo delay in logic path determins the max speed of operation of digital logic circuit
    SETUP: 
       a. Clock cycle needs to accomodate the propagation delay, combo delay and setup slack
    ![image](https://github.com/user-attachments/assets/b590369a-5599-4321-90f2-4aa8cfde7e9b)
       b. For maximum performance, we need the cells faster for Setup 
    HOLD:
       a. Now for data to be held at the launch side for the data to be reliably captured. 
       b. We now need slow cells for this performace requirement
    5. Load in Digital Logic Circuit is known as Capacitance
       a. Faster charging . discharging of capacitance is less cell delay
       b. For this we need transistors capable of more current. Ex: SVT, LVT, HVT cells
       c. This changes according to the technology nodes for optimizing area, power.
    6. Now to guide the synthesis to pick up the required transistors, we need constraints
    7. Below shows how a basic conversion looks like
    ![image](https://github.com/user-attachments/assets/71fc2178-ee53-4d5f-a0e4-f75a0e303a3a)

    
# DAY 2: Introduction to timing Libs
### Introduction to dot lib
  1. The lib contains certain initial data for specific PVT (Process, Voltage and Temperature)
  2. These are variations that happens in fabrication.
  3. In order for the chip to function after fabrication, there needs to be best and worst limits where it can oprate efficiently in terms of performance and consisitency
  4. So when designing, the libs will be characterized to mimic these PVT variations
     ![image](https://github.com/user-attachments/assets/e094eb7a-8c00-47bd-8d49-df29dd45427b)
     ![image](https://github.com/user-attachments/assets/67c74ed2-2880-4580-be92-7ebc3b1cef97)
  5. Cell deifination will be provided which can be used for this PVT characteristics
     ![image](https://github.com/user-attachments/assets/eb7cc71f-82ee-42d1-8a2d-a77187ecc44b)
       a. Will include cell features like leakage, inputs, outputs and how the gate is paired with different logic gates
  6. Area also changes as the bigger cells are used
  7. Delays will also be different for the same
  8. The Power usage also increases



