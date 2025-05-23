# DAY 1: Introduction to Verilog RTL design and Synthesis

## Introduction to open-source simulator iverilog

Installation of the resource and tools required for the workshop

  1. Gitclone the repository
  ![image](https://github.com/user-attachments/assets/c358a909-8448-4dea-9b9e-81197be2cf21)

  ![image](https://github.com/user-attachments/assets/b9661e6e-1735-47d1-adab-f84387adca0c)

  2. Check the input libs, verilog file
  ![image](https://github.com/user-attachments/assets/cc27dba1-2e53-46b6-a251-83de2a25a614)

  3. Install iverilog
  ![image](https://github.com/user-attachments/assets/cf0e336c-b4f0-4170-9ece-bc72006c97b0)

  4. Install gtkwave
  ![image](https://github.com/user-attachments/assets/b8a1b8f9-2365-4e27-a347-2e6404e08adf)



### Introduction to iverilog design test bench

  1. Launch the iverilog along wth the test bench
     ![image](https://github.com/user-attachments/assets/9f4dbf11-09bb-47f4-8985-76e6c1591d28)
  
  2. Use gtkwave for the .vcd file and confirm the logic
     ![image](https://github.com/user-attachments/assets/3abdd00d-45bb-46d0-9172-813d1193f429)

     ![image](https://github.com/user-attachments/assets/f388b2ef-d2ee-4c65-9abd-5f545f0ee596)

     ![image](https://github.com/user-attachments/assets/40524a81-03af-4e81-80ea-54b48ed74113)



### Labs using Yosys and Sky130 PDKs
  
  1. Launch Yosys in verilog_files directory
     ![image](https://github.com/user-attachments/assets/b419bcb0-d923-4494-989b-73f1c8fd211d)
     
  2. Now read the lib and the netlist for the good_mux
     ![image](https://github.com/user-attachments/assets/bf6101af-b220-4624-8e29-c1982331bc7b)

     ![image](https://github.com/user-attachments/assets/d24d0aca-8b24-47c8-a96a-2407888c9475)

  3. The top module is good_mux which reads it from the netlist
     ![image](https://github.com/user-attachments/assets/6155161c-335a-4176-8bf8-e5b4f02c610f)

  4. No proc in the good_mux file, so this is only a combo logic
     ![image](https://github.com/user-attachments/assets/60710496-659c-4db9-a336-3e4df6e8a209)

  5. Generate the RTL netlist for this module. THis will be realised using the .lib file which as the cells/ gates required to complete the logic
     ![image](https://github.com/user-attachments/assets/082336f1-f92b-4953-9bdd-1f2baf77ed2d)

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
  
  1. Invoke the Yosys and read the lib
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


  ### Ex: dff_const3
  
  ![image](https://github.com/user-attachments/assets/5659947a-bf85-4b45-9095-d15e939ed13c)

    1. Upon reset, Q = 1 and Q1 = 0. Then the Q1 does not change after the reset
    2. The output Q will be high except for 1 clock cycle. This makes the circuit unpotimized
  Check this in iverilog
  ![image](https://github.com/user-attachments/assets/881f03c5-534e-4467-ad5f-83afafbc7915)
  
  ![image](https://github.com/user-attachments/assets/7aa6df5a-8654-42dc-ab2a-6e442e5202f9)


  #### In yosys:
  
  ![image](https://github.com/user-attachments/assets/dc6a6842-692f-4526-a3d9-f5f676f2ce20)
    
    a. dff cells are taken
  
  ![image](https://github.com/user-attachments/assets/b9f2be30-312f-4de9-a9d3-70ab89bb53f7)

  ![image](https://github.com/user-attachments/assets/37691449-597f-453b-a896-8f1589f2cd98)
    
    a. Mapped inverter and used flops
    b. Output check
    
   ![image](https://github.com/user-attachments/assets/70c892f8-ff0e-4e46-863f-9f29720ce05a)

```NOTE: 
      i. When show is done without abc -liberty, then bth were connected to reset. Now it is properly connected as per the logical connection
      ii. For set and reset, inverter is used
```
    3. Not every constant connection in dff will be optimized


  ### Ex: dff_const_4
  
  ![image](https://github.com/user-attachments/assets/78f99172-1a2b-454c-862d-afaa6b10237f)

  #### In iverilog:
 
  ![image](https://github.com/user-attachments/assets/74a0d92b-3199-4f18-8a97-98aa1a24d7a7)
      a. When the reset goes to zero, the q and q1 stays the same uneffected by the reset

  #### In Yosys:
  
  ![image](https://github.com/user-attachments/assets/92ae4fef-dbcb-41a9-b1d3-1a2db7457ef3)
      a. Zero cells used for optimization
    ![image](https://github.com/user-attachments/assets/b994c380-5654-4b8c-912c-4096a6ba982a)
      b. After abc -liberty also the optimization remains the same

  ### Ex: dff_const5
  
  ![image](https://github.com/user-attachments/assets/501841c1-0859-44cd-83d1-19206036e6c0)

  #### In iverilog:
  
  ![image](https://github.com/user-attachments/assets/80ee0b1d-3184-4bdc-83e6-323eeecc5d57)
      a. When the reset is 0, there is no change in the Q and Q1 values.
      b. Only when the clock edge changes, Q1 is 1
      c. And when the clock has completed one cycle, the Q value is 1
      b. After this, both the Q and Q1 values stay constant

  #### In Yosys:
  
  ![image](https://github.com/user-attachments/assets/0cdb3c1c-f032-40b8-8434-7933cdf133e5)
      
      a. 2 flops are syntheszed
  
  ![image](https://github.com/user-attachments/assets/78eb1ce9-fd26-4584-b6da-c489cf6e79d6)
    
  ![image](https://github.com/user-attachments/assets/65c3a429-e619-47b9-bef7-8a8cc7937ae5)
      
      b. Outputs synthesized as seen in iverilog


  ## Sequential optimization with unused outputs
  
  ### Ex: Counter opt
  
  ![image](https://github.com/user-attachments/assets/75d8f316-49b2-4181-8088-ab1b91f0c471)

  #### In iverilog:
  
  ![image](https://github.com/user-attachments/assets/ce2daea1-4b34-4df8-8b45-8159acd0e1cd)
    
    1. The toggling of Q continues as the clock cycle gets completed

  #### In Yosys:
    1. Inferring only 1 flop but it has three bit count and should have had 3 flops
  
  ![image](https://github.com/user-attachments/assets/5ffae940-2c70-4f61-b287-8dd57a6b342f)
    
    2. Toggling is happening and the unused outputs are optimized
  
  ![image](https://github.com/user-attachments/assets/f4d7b6ab-9a88-469b-a22e-1a7af4e748c0)
    
  ### Ex: Count opt 2 with 3 bits as counter value
  
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

  1. If statement always translates into a MUX
     
### Incomplete If
  
  ![image](https://github.com/user-attachments/assets/37bfdcf2-9f8a-4583-a15a-c6a4a91f644d)

  1. Since else condition is not given, it will behave like D-Latch

#### In iverilog

![image](https://github.com/user-attachments/assets/59f73afe-9087-4797-9838-964151dada73)
  
  1. Whenever, i0 is high, Y changes and vice-versa
  2. When i0 goes low, Y latches on the previous data and doesnot change


#### In Yosys

![image](https://github.com/user-attachments/assets/3d134afc-2c9a-408b-aaf0-c62934536b00)
  
  1. Aim was to code a MUX, but tool gave a latch instead

![image](https://github.com/user-attachments/assets/c1ed7cc6-86fb-4c12-a285-52684fc3f35f)
  
  2. i2 is unused, i0 is en and i1 is D pin just like latch

### Incomplete If 2

![image](https://github.com/user-attachments/assets/356c0203-3d92-41c2-b55c-916066a7c41c)
  
  1. Else condition is not given and the condition will latch onto Y and keep the previous value

#### In iverilog

![image](https://github.com/user-attachments/assets/db5cb2bf-63d6-41ab-b1bd-2c453829639e)

  1. When i0 is high, Y = i1
  2. WHen i1, i0 is low, output is constant
  3. When i2 is high, it follows i3

#### In Yosys

![image](https://github.com/user-attachments/assets/8b3d2f05-e254-47a8-abb4-6476e8d8840a)

![image](https://github.com/user-attachments/assets/c24f0564-ae6f-4f2c-8d63-d36ae511ce39)


### Incomplete Case
  1. Select is a 2 -bit signal
  2. Since the default is not added, it will latch

#### In iverilog
  1. When sel[1] = 1, value is latch. otherwise it should be not used

![image](https://github.com/user-attachments/assets/bbb75fad-12f0-4d57-b34c-d437c3343238)

  3. When sel[0], it follows i0

![image](https://github.com/user-attachments/assets/517bd245-42db-4457-8eaf-e7177a2f3d89)


#### In Yosys

![image](https://github.com/user-attachments/assets/cad32b2c-d523-4ad0-9408-ec6af5b4617f)

![image](https://github.com/user-attachments/assets/8b182538-e6b6-47f3-8782-f5b649bb7678)



### Complete Case

![image](https://github.com/user-attachments/assets/88311982-59af-402a-a7b2-a722b67eebb3)
  
  1. Has default

#### In iverilog

![image](https://github.com/user-attachments/assets/728fbb71-ad61-44bc-adb8-1569c837b35f)
  
  1. The inputs behave as intended

#### In Yosys

![image](https://github.com/user-attachments/assets/3770f031-9c66-42c2-8298-d1e2c2ec6e8c)

![image](https://github.com/user-attachments/assets/ae1ee0e5-fd28-4018-891c-6984e01c62dd)
  
  1. Even with default case, inferred latech cannot be completely avoided
  2. When sel[0]&sel[1] both = 1


### Partial case

#### In Yosys

![image](https://github.com/user-attachments/assets/68abbdfc-77b2-45b1-a279-e72809a03fe2)

![image](https://github.com/user-attachments/assets/e16ef474-6cb6-4dac-94de-f6558fd77a7c)


### Bad case

![image](https://github.com/user-attachments/assets/e44eae2f-c22e-46c7-b0b2-7ee959c1b8d5)
 
  1. When sel[0]/ sel[1] , can can get the y value
  2. Now when for one output, multiple data is written, overlas occur
  3. Since there are no missing cases, it will not cause any inferred latches

#### In iverilog

![image](https://github.com/user-attachments/assets/bc3723e5-9c04-4095-be22-f1f613960b3c)


#### In Yosys

![image](https://github.com/user-attachments/assets/488b35df-afac-451b-aa6b-9598eb011ef9)

![image](https://github.com/user-attachments/assets/8f70f6cd-02fc-4252-9016-6142f9ab33d3)

#### In GLS

![image](https://github.com/user-attachments/assets/d20e6812-16eb-464c-9e51-b7983c7e5c23)

![image](https://github.com/user-attachments/assets/6f8cb735-e65b-4ae6-bf66-e26f661afa1e)
  
  1. Data is getting update in Y as per the expectation for the inputs



## For and for generate constructs

### For loops

#### Ex: MUX

![image](https://github.com/user-attachments/assets/a98255d6-fa98-4c8d-b49b-f76b1f854750)

##### In iverilog
  1. The sel[0], Y = i[0]
  2. sel[1], Y = i[1]
  3. sel[2], Y = i[2] and so on

![image](https://github.com/user-attachments/assets/bbd24d2d-3e15-4fea-b5b8-8900bb5e897e)

  4. If case statement would have been used, small bit code will be simple and less lines, but if the bit increases, then writing n number of lines is time consuming (Ex: 256x1;1024x1 MUXs)

##### In Yosys

![image](https://github.com/user-attachments/assets/b46da859-8dd9-4daa-b63c-629ce8b41a8c)

![image](https://github.com/user-attachments/assets/cc675a80-672e-4f9c-92cf-c7f488eb7cee)

##### In GLS

![image](https://github.com/user-attachments/assets/e8ff4b0c-dda5-4d3a-938c-6ec4adb7cc46)

![image](https://github.com/user-attachments/assets/0885d2b9-1d26-4441-9d81-758527727fd2)



#### Ex: DEMUX

![image](https://github.com/user-attachments/assets/73be9e34-b0fb-4259-a4cd-d85fafff4301)

  1. All the outputs to be instantiated to 0 first. As per the sel[i], will follow the input signal
  2. Case will avoid inferred latches when all the y is assigned to the input bits. But with increase in bit levels, lines will also increase to assign the 'y' for all the 'i'

##### In iverilog

![image](https://github.com/user-attachments/assets/076b21d7-63dc-43c8-8c5c-59dd6c06e1cb)

##### In Yosys

![image](https://github.com/user-attachments/assets/89a74cb8-b4e4-4eff-b91e-77f4c116795c)

![image](https://github.com/user-attachments/assets/01cc023f-eab4-4a6a-b367-83dfa7e607f7)

##### In GLS

![image](https://github.com/user-attachments/assets/898725ad-fb6e-40ba-bc8e-a7001fa8226d)

![image](https://github.com/user-attachments/assets/a3d70088-0f49-4e77-a1fc-403d887c7a69)


#### Ex: Ripple Carry adder

![image](https://github.com/user-attachments/assets/7c50e4a8-5ec3-4e32-8241-b955e613dd70)

![image](https://github.com/user-attachments/assets/7ec25e4d-0092-4f66-9370-4e0ae34ec9c1)

  1. Can be broken down to be full adder separately which can add and give sum and carry
  2. Each full adder has 3 inputs for 3-bit and has 1 carry and 1 sum
  3. Each carry is connected to the next full adder's input MSB

![image](https://github.com/user-attachments/assets/c0bc7aa5-2297-4c99-a008-b436b3e58c97)


##### In iverilog

![image](https://github.com/user-attachments/assets/2fc5e5dd-d72d-4318-b71c-0f5030c123d0)
 
  1. Since full adder is called but it is not instantiated with this so the modules it is unable to find
  2. Need to read the fa.v also
  
  ![image](https://github.com/user-attachments/assets/06d689f0-16cd-46c2-b946-a69fae37eec4)

  3. Change to decimal format

  ![image](https://github.com/user-attachments/assets/4b18432a-3bfe-4358-a6b8-03d7142f18e4)


##### In Yosys

![image](https://github.com/user-attachments/assets/5178968c-64a5-4785-8a8c-a8e039506c13)

![image](https://github.com/user-attachments/assets/74304563-5a0a-4f6c-a2b5-919ccf7bf960)

RCA

![image](https://github.com/user-attachments/assets/10aaf04d-a2f9-4ee1-863a-c63c4070025e)

FA

![image](https://github.com/user-attachments/assets/f4e74a4b-b787-42d7-ad34-66cb43e9ab92)


##### In GLS

![image](https://github.com/user-attachments/assets/93c4ecfc-98a3-4481-9ab6-ead14dd9049d)

![image](https://github.com/user-attachments/assets/1ff7146d-b7e4-4df9-9fbd-17ffb18e324f)

![image](https://github.com/user-attachments/assets/cf06a386-8bf2-4174-a906-285d2bb70092)

![image](https://github.com/user-attachments/assets/c5bc3b15-2370-4c4e-a135-cea686f6657a)



































