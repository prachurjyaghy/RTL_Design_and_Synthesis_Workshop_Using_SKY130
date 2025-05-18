# DAY 1: Introduction to Verilog RTL design and Synthesis

## Introduction to open-source simulator iverilog

### Introduction to iverilog design test bench


### Labs usign Yosys and Sky130 PDKs
  1. Launch Yosys in verilog_files directory
  2. Now read the lib and the netlist for the good_mux
  3. The top module is good_mux which reads it from the netlist
  4. No proc in the good_mux file, so this is only a combo logic
  5. Generate the RTL netlist for this module. THis will be realised using the .lib file which as the cells/ gates required to complete the logic
  6. The final shows the inputs and outputs
     ![image](https://github.com/user-attachments/assets/36c34cbe-4374-4f3b-a5e8-1b6709aac5a7)
  7. Show will display the process
     ![image](https://github.com/user-attachments/assets/489899b3-e5cb-4ef7-80d0-0de957cdb926)
     ![image](https://github.com/user-attachments/assets/dfa0fbd6-4688-4abd-86b2-712f6dd96001)
  8. Test Bench netlist created for gate level
     ![image](https://github.com/user-attachments/assets/029041ab-1b4b-48df-a0bd-d6df0f5e7113)
     ![image](https://github.com/user-attachments/assets/7d602651-bc90-4165-8ff6-6c7efd6d400c)
  9. Simplified netlist
      ![image](https://github.com/user-attachments/assets/3f403465-5bf7-4ac0-a017-c00b206957cd)
      ![image](https://github.com/user-attachments/assets/6a707977-4219-4e43-91c6-b233b885ecbd)
  10. Check the connections, the wires, inputs and how they are assigned in the final gate netlist
  11. Top module is same as what we checked in the original netlist before the synthesis


# DAY 2: Introduction to Timing .libs
## Introduction to dot Lib
  ![image](https://github.com/user-attachments/assets/b3b8975d-a6a3-4247-a8b7-0785fadb83d2)

  1. Open the corresponding verilog for the gate
     ![image](https://github.com/user-attachments/assets/8f955868-0d3f-43a9-a753-31e5c62afb9f)
  2. We can check the data for the multiple conditions
     ![image](https://github.com/user-attachments/assets/aec75d21-e395-4ed3-9b15-d8d9f963251e)
  3. Area also increases
     ![image](https://github.com/user-attachments/assets/92b47991-877d-4702-9d41-a563532df3ef)
     





