![image](https://github.com/user-attachments/assets/5bc1bb41-eaba-4898-b68b-5c8b6a35b915)# DAY 1: Introduction to Verilog RTL design and Synthesis

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
     
## Hierarchical vs Flat Synthesis
  ![image](https://github.com/user-attachments/assets/0898f993-0f32-4fc0-bc47-d432228d240f)

### Hierarchical
  1. INvoke the Yosys and read the lib
  2. Then read the verilog
     ![image](https://github.com/user-attachments/assets/db39c3dc-8a8d-45ef-ad3b-083ddd985df9)
  3. Do the synth -top multiple_modules
     ![image](https://github.com/user-attachments/assets/7ad62ed4-e644-42cc-a47d-fec375712d96)
  4. Do the abc -liberty of the lib
     ![image](https://github.com/user-attachments/assets/93571de6-ece2-4cf0-91d3-338afe2ee6bf)
       -> Since there are multiple modules, need to select the submodule too 
     ![image](https://github.com/user-attachments/assets/cd7b3001-505a-4a30-8f48-a0aa6d6ec716)
  5. Use the below command for showing all the hierarchies
     ![image](https://github.com/user-attachments/assets/a1733150-03dd-4b4f-9c40-dc2d853001a8)
  6. Now get the netlist
     ![image](https://github.com/user-attachments/assets/e2aff738-1322-4b24-91a8-02b2f3e51f96)
     ![image](https://github.com/user-attachments/assets/798098cf-5e77-4baa-9604-e7f2af12ae8d)
  7. In the netlist, the hierarchies are preserved
     ![image](https://github.com/user-attachments/assets/00fc2647-5f85-480f-b17b-3c615db202ad)

### Flat
  ![image](https://github.com/user-attachments/assets/9fdfe0d0-15ce-4156-b7f4-1c678e086ad0)
  1. Instantiation is seend directly defined under the main top multiple_module
     ![image](https://github.com/user-attachments/assets/eeb172c6-d724-494e-986b-d480b486275f)
  2. Now flatten it
     ![image](https://github.com/user-attachments/assets/04151a5d-a9af-45c7-bdfe-15521ca25c72)
     ![image](https://github.com/user-attachments/assets/f06fc628-0e7d-4802-b1ae-6d3d17513601)
  3. Try to separate the submodules and do the synthesis
     ![image](https://github.com/user-attachments/assets/063da6e1-3986-4a7d-a2a9-b0c16cd8acca)
      - Submodule1 
     ![image](https://github.com/user-attachments/assets/336f86cc-684f-4866-bd58-dc1cc6f68f5d)

### Flop Synthesis
  
  #### Async reset
  ![image](https://github.com/user-attachments/assets/5efd0656-b739-4882-b567-5c822c3e6166)
 
  1. D is Q when the reset and waited for the clock edge to change the value
     ![image](https://github.com/user-attachments/assets/9be15cb9-95eb-4ef4-966c-3b899b61bdfc)
  2. The Q value stays equal to D as an when the clock signal posedge is received. Async is changes the value of Q to low immediately when it arrives but is not changing back due to the clock edge
     ![image](https://github.com/user-attachments/assets/74d2da57-d1bd-4927-a8b6-1a7fa3397cfc)

  #### Async set  
  ![image](https://github.com/user-attachments/assets/dec4ff5a-3951-4955-b97d-4e314d1bcae6)

  1. The changes in the D pin upon the edge of the clock. Set is enabled, the Q was 0.
  2. Now as and when the clock edge changes, the D value changes the value of Q as well
     ![image](https://github.com/user-attachments/assets/ad27104f-3d2c-49da-a880-31417ac44e2c)
  3. Now whenn the sync is set, irrespective of clock, it is keeping the Q value as 1. D is not effected
     ![image](https://github.com/user-attachments/assets/ae118e05-7aa1-476b-ad24-6b06387530c1)

  #### Sync reset
  ![image](https://github.com/user-attachments/assets/7c7cba21-fb9a-4f42-9885-59629ae57b3c)

    1. THe output Q is going until the next clock edge and then changing
    2. The reset is getting applied only on the posedge of the clock
    ![image](https://github.com/user-attachments/assets/3d9fa9ee-0de7-4816-8c03-ab46e75daf95)

    3. Reset is taking high precedence over the D as the code is written with always as priority
    ![image](https://github.com/user-attachments/assets/4ac3ac16-10ee-43a4-953b-e04ff00ef9ee)



  












