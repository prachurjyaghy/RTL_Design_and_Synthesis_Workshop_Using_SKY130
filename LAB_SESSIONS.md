# DAY 1: Introduction to Verilog RTL design and Synthesis

## Introduction to open-source simulator iverilog

### Introduction to iverilog design test bench


### Labs using Yosys and Sky130 PDKs
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

### Flop Synthesis in iverilog
  
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
  ![image](https://github.com/user-attachments/assets/5a864c2a-72fa-46a8-b510-ad56028a449b)

    3. Reset is taking high precedence over the D as the code is written with always as priority
  ![image](https://github.com/user-attachments/assets/336e5df5-4721-473c-ac6f-e39b38d8851a)


### Yosys synthesis
#### Async reset

![image](https://github.com/user-attachments/assets/3025069b-8c5a-4a14-9352-dc40152ab076)
  1. Looking only to the dffs
     ![image](https://github.com/user-attachments/assets/3c32c126-71a6-4a75-b0f8-8fe76d7c6e06)
     ![image](https://github.com/user-attachments/assets/53aa2c4f-720a-400f-9699-10f01fb06311)
     
  2. Inverter is used because code is written as active high reset, but flop has active low reset and the A_bar will cancel itself
  ![image](https://github.com/user-attachments/assets/79505560-b65d-4fea-97e3-bbec690d45ea)


#### Async set
![image](https://github.com/user-attachments/assets/daf31c29-36ae-4dfd-bbb7-21211b8c1373)
![image](https://github.com/user-attachments/assets/3865c5e0-a564-4091-b939-83ea7753789e)

#### Sync reset
![image](https://github.com/user-attachments/assets/0d3e5293-e2d3-4ba8-8f8f-dae6d8cc5737)

![image](https://github.com/user-attachments/assets/b87ecd4a-d5bb-472b-9c9c-51f7b272972e)


### Interesting Optimizations
#### Mult2  
  1. Number of cells inferred is 0
     ![image](https://github.com/user-attachments/assets/536c9e1b-64bd-4586-bd09-bf881ac34d0d)
  2. There is nothing to create for cell
     ![image](https://github.com/user-attachments/assets/12c4feb8-cae3-456b-a9f3-c7a403621191)
  3. Number 'a' appended with zero
     ![image](https://github.com/user-attachments/assets/21713c7d-46df-4e9c-85be-16c029ae383d)
     ![image](https://github.com/user-attachments/assets/82e5956b-cd85-4889-8d4d-1168f0215f2d)

#### Mult8
  ![image](https://github.com/user-attachments/assets/3bd13e1b-f0d9-47a3-a385-ef5bb0d2c4a1)
  ![image](https://github.com/user-attachments/assets/bd4f5599-5e90-43f4-bcac-b8045470b8b4)
  ![image](https://github.com/user-attachments/assets/3765a3c1-2b30-4190-8eb6-5e793b6d6067)
  1. These optimizations may not require standard cells and can be mapped using wires only



# DAY 3: Introduction to Optimizations

## Combinational Logic
  ![image](https://github.com/user-attachments/assets/8f7a70c9-15fd-4bdd-a525-e86ca2e8acae)

  1. Follow the same process for synthesis in yosys
     ![image](https://github.com/user-attachments/assets/d2902a05-4676-4e9c-9ce5-1b46be1b13bc)
  2. Now for the propagation delay and optimization in yosys
     ![image](https://github.com/user-attachments/assets/b790e855-d410-464a-b4e1-94c51997cfc5)
     ![image](https://github.com/user-attachments/assets/61023e47-db9a-4e8d-b8c7-380ccd80c297)
  3. Check the result to find the AND gate
     ![image](https://github.com/user-attachments/assets/8d8f6e59-3fc2-4cfe-a267-fd46b93c7f9e)
  4. Now check the same for the opt_check2
     ![image](https://github.com/user-attachments/assets/34b92e08-6e71-498a-98d6-ae20ec240704)

  5. Check the same for opt_check3 doing the whole synthesis process
     ![image](https://github.com/user-attachments/assets/55c3cef2-8084-4556-8283-d1c5fd8ce5c5)
  6. Multiopt. Needed to flatten the design
     ![image](https://github.com/user-attachments/assets/9fc8b9f1-29a2-408b-bc4b-42902582a417)

     ![image](https://github.com/user-attachments/assets/d59a4898-4f13-44c3-8def-173a4fee2601)


  ## Sequential Optimization
  ![image](https://github.com/user-attachments/assets/7d4ff4b1-2f4b-4824-9a8c-db292c406bf1)
    1. dff lib map is used for the library that needs to be used
    2. Execute the netlist exactly like the way in combo opt process
       ![image](https://github.com/user-attachments/assets/26746b23-17e2-4e21-b55c-a6b495614c7f)
       ![image](https://github.com/user-attachments/assets/f5f25402-1e91-4958-a596-90ad5741ab45)

    3. Check the output
  ![image](https://github.com/user-attachments/assets/45ba57fa-da1f-4719-8c16-633bf8a9f944)
    
    4. Library is expecting an active low reset, but it is codded as active high. So inverter is used before the flop

    5. Check for the dff_const2 which has the following data already mapped
   ![image](https://github.com/user-attachments/assets/0897e7b9-d303-4a65-9842-4aa307276b46)

    6. Check the output as the cells for dff is not synthesized as the value is already constant
   ![image](https://github.com/user-attachments/assets/14099038-a8ac-4683-9b47-52b401320e72)


  Ex: dff_const3
  ![image](https://github.com/user-attachments/assets/5659947a-bf85-4b45-9095-d15e939ed13c)

    1. Upon reset, Q = 1 and Q1 = 0. Then the Q1 does not change after the reset
    2. The output Q will be high except for 1 clock cycle. This makes the circuit unpotimized
  Check this in iverilog
  ![image](https://github.com/user-attachments/assets/881f03c5-534e-4467-ad5f-83afafbc7915)
  ![image](https://github.com/user-attachments/assets/7aa6df5a-8654-42dc-ab2a-6e442e5202f9)

  In yosys:
  ![image](https://github.com/user-attachments/assets/dc6a6842-692f-4526-a3d9-f5f676f2ce20)
    a. dff cells are taken
  ![image](https://github.com/user-attachments/assets/b9f2be30-312f-4de9-a9d3-70ab89bb53f7)

  ![image](https://github.com/user-attachments/assets/37691449-597f-453b-a896-8f1589f2cd98)
    a. Mapped inverter and used flops
    b. Output check
    ![image](https://github.com/user-attachments/assets/70c892f8-ff0e-4e46-863f-9f29720ce05a)

  NOTE: 
      i. When show is done without abc -liberty, then bth were connected to reset. Now it is properly connected as per the logical connection
      ii. For set and reset, inverter is used

    3. Not every constant connection in dff will be optimized


    Ex: dff_const_4
  ![image](https://github.com/user-attachments/assets/78f99172-1a2b-454c-862d-afaa6b10237f)

    In iverilog:
  ![image](https://github.com/user-attachments/assets/74a0d92b-3199-4f18-8a97-98aa1a24d7a7)
      a. When the reset goes to zero, the q and q1 stays the same uneffected by the reset

    In Yosys:
  ![image](https://github.com/user-attachments/assets/92ae4fef-dbcb-41a9-b1d3-1a2db7457ef3)
      a. Zero cells used for optimization
    ![image](https://github.com/user-attachments/assets/b994c380-5654-4b8c-912c-4096a6ba982a)
      b. After abc -liberty also the optimization remains the same

    Ex: dff_const5
  ![image](https://github.com/user-attachments/assets/501841c1-0859-44cd-83d1-19206036e6c0)

    In iverilog:
  ![image](https://github.com/user-attachments/assets/80ee0b1d-3184-4bdc-83e6-323eeecc5d57)
      a. When the reset is 0, there is no change in the Q and Q1 values.
      b. Only when the clock edge changes, Q1 is 1
      c. And when the clock has completed one cycle, the Q value is 1
      b. After this, both the Q and Q1 values stay constant

    In Yosys:
   ![image](https://github.com/user-attachments/assets/0cdb3c1c-f032-40b8-8434-7933cdf133e5)
      a. 2 flops are syntheszed
    ![image](https://github.com/user-attachments/assets/78eb1ce9-fd26-4584-b6da-c489cf6e79d6)
    ![image](https://github.com/user-attachments/assets/65c3a429-e619-47b9-bef7-8a8cc7937ae5)
      b. Outputs synthesized as seen in iverilog


  ## Sequential optimization with unused outputs
  Ex: Counter opt
  ![image](https://github.com/user-attachments/assets/75d8f316-49b2-4181-8088-ab1b91f0c471)

  In iverilog:
  ![image](https://github.com/user-attachments/assets/ce2daea1-4b34-4df8-8b45-8159acd0e1cd)
    1. The toggling of Q continues as the clock cycle gets completed

  In Yosys:
    1. Inferring only 1 flop but it has three bit count and should have had 3 flops
  ![image](https://github.com/user-attachments/assets/5ffae940-2c70-4f61-b287-8dd57a6b342f)
    
    2. Toggling is happening and the unused outputs are optimized
  ![image](https://github.com/user-attachments/assets/f4d7b6ab-9a88-469b-a22e-1a7af4e748c0)
    
  Ex: Count opt 2 with 3 bits as counter value
  ![image](https://github.com/user-attachments/assets/a6522ee4-3520-4529-8fd1-593615d8e407)

    1. Able to see the 3 DFF after synth
  ![image](https://github.com/user-attachments/assets/14e35bc0-0f04-4622-96e6-b590ce63b56c)
    2. Output with 3 DFFs
  ![image](https://github.com/user-attachments/assets/762793fc-3784-4ad0-be6c-34aaac44ba89)



# DAY 4: GLS, Blocking vs Non-Blocking and Synthesis Simulation Mismatch

## GLS and Synthesis Simulation Mismatch
Files to execute and check for GLS
![image](https://github.com/user-attachments/assets/bd90b445-f70d-425f-828c-643c0cc2deeb)

### Ex: Ternary operator:
#### In iverilog
  Behaves as a 2:1 MUX
  ![image](https://github.com/user-attachments/assets/3bbe1da0-bd00-4314-aa05-69c4f65cf810)
#### In Yosys
![image](https://github.com/user-attachments/assets/a0cd4460-f435-48b5-9898-d25974c600d2)
![image](https://github.com/user-attachments/assets/50b04537-b876-41a2-a2ea-b2f247b4cd28)

#### In GLS
![image](https://github.com/user-attachments/assets/6c83109c-7228-44c4-9b80-608bb42624b0)
Load the gate netlist in iverilog
![image](https://github.com/user-attachments/assets/ee798d00-6cf7-4a6f-944b-d4c142792f05)
![image](https://github.com/user-attachments/assets/9420d625-ab4c-48d7-bf6f-99f729df8e65)

### Ex: Bad MUX
  1. Deliberately, as always(sel) will only execute for sel and behave like flop
#### In iverilog and gtkwave
  1. i0 is not changing with respect to sel and toggling, so Y is 1
  2. Only when sel is changing, Y changes
     ![image](https://github.com/user-attachments/assets/ee02684a-2b68-48ae-95fe-be72085c082c)

#### In Yosys
![image](https://github.com/user-attachments/assets/f2a177cd-885d-4450-99c4-51077ff654c4)

#### In GLS
![image](https://github.com/user-attachments/assets/51e4149f-4123-449a-bc26-4d5ca9284706)
![image](https://github.com/user-attachments/assets/cf10aba7-6e50-4e75-85a9-fb4c3204dec1)


### Ex: Blocking caveat
![image](https://github.com/user-attachments/assets/29454667-43e3-4465-919c-ad5e4080442f)

#### In iverilog
Previous data of d is old when the toggling happens
![image](https://github.com/user-attachments/assets/b0d39228-ef67-4897-87b3-fffab9168473)
![image](https://github.com/user-attachments/assets/6aa5e35a-fa17-424f-9d4e-10f0f1ef14e0)
![image](https://github.com/user-attachments/assets/208766c2-0c3f-436d-819d-79c3607eb89e)


#### In  Yosys
![image](https://github.com/user-attachments/assets/4b228059-1e50-43dd-a094-493c0bdd2d0e)
![image](https://github.com/user-attachments/assets/ad48b646-8c56-42bb-a7e3-2da993203131)

#### In GLS
![image](https://github.com/user-attachments/assets/495b45eb-036a-4632-987c-339e9ff0f70f)
This is clearly synth-sim mismatch and caused by blocking statement
![image](https://github.com/user-attachments/assets/b5c3841e-63cd-4a1b-b060-808e7fcebb63)




# DAY 5: Optimization in Synthesis
## If Case constructs





















