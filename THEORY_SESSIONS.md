# DAY 1: Introduction to Verilog RTL design and Synthesis

## Introduction to open-source simulator iverilog

### Introduction to iverilog design test bench

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
  ![image](https://github.com/user-attachments/assets/b590369a-5599-4321-90f2-4aa8cfde7e9b)
    
    SETUP: 
       a. Clock cycle needs to accomodate the propagation delay, combo delay and setup slack     
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

### Hierarchical vs Flat Synthesis
  
  ![image](https://github.com/user-attachments/assets/21b68407-43a3-43ac-8a1f-5e93130d9355)

  ![image](https://github.com/user-attachments/assets/7849219b-8ade-4a6c-a66f-73a66be80d92)

#### Hierarchical
  1. The modules are inside a main function and called.
  2. The logic output can use these basic sub modules to create another logic
  3. In the output, the required gate is not as per the original theory gates
  4. As per Demorgan thoeram, the NAND is used as a univeersal gate
  5. Synthesis does not want to use stacked PMOS(as it has lower mobility & if it needs to be used, then a larger cell has to be used instead)

#### Flat Synthesis
  1. We can separately can create netlist for the sub modules too
  2. If this submodule is being now used by multiple top modules. We do not need to write them in all of the modules. It can be replicated.

     ![image](https://github.com/user-attachments/assets/d3f23579-a943-46f9-906e-531fce7b18b7)
  
  3. In yosys, synth -top <module_name> command is used

### Various Flop Coding Styles and optimization
  1. As per the input, output is going to change as per the propagation delay and may give Glitch
  2. The glitch can be avaoided in combo circuits using flops. Since flops are edge triggered only, then the signal is preserved
  3. We need to initialize the flop using reset / set. They can be either sync or async

![image](https://github.com/user-attachments/assets/8bec6fc5-99ad-4b5c-a9d6-f1065743177e)
  
  Ex: for posedge clock
      a. Asyync means irrespective of clock
      b. Data is set due to the async_set
      c. Sync means it is on the D pin of the flop. It awaits for the clock edge
      d. Upon clock posedge, the sync_reset is executed

  Ex: Both async and sync reset
  
  ![image](https://github.com/user-attachments/assets/1084ea7b-75be-43c3-af5c-fa93a4fffdae)
  ![image](https://github.com/user-attachments/assets/3838660d-44f4-4561-806d-4ccd2c069795)

#### Interesting optimizations
![image](https://github.com/user-attachments/assets/b19aabc3-b3e5-4f77-94bb-7f4d164caa21)
  
  1. WHen the above mult does not mean using mux but basic binary multiplication.
  2. Simple conversion from a[2:0] to y[3:0]


# DAY 3: Combinational and sequential optimizations  

## Optimizations 
  1. To get the most optmized design in Area and Power
  2. Constant propagation with direct opt
  3. Boolean Logic Optimization using K-MAP or Quine algos

Ex: Constant Propagation using transisters

![image](https://github.com/user-attachments/assets/86b8bd7a-2595-4688-b19c-af7ce37c2b73)
    
    a. As A is propagated as 0, it got optimized to inverter 

Ex: Boolean Logic Optimization

![image](https://github.com/user-attachments/assets/f2f6b862-3530-4c07-ac43-3de1ba4d8dca)
    
    a. Reduction for the logic

### Sequential optimizations
#### Sequential constant propagation
  ![image](https://github.com/user-attachments/assets/721795ca-666d-420b-9da5-fd386616d609)

  1. Id reset is enabled, Q =0. Or else, Q = 0 as D = 0. Q is always 0 even with clock propagation
  2. The Q value goes to the gate which becomes a.0_bar = a_bar + o_bar = a_bar+1 = 1. Y = 1 always
  3. Id set is connected to the flop and the logic remains same for the gate
     ![image](https://github.com/user-attachments/assets/73f02dfe-e81a-40e0-9359-a10d1cc27bfd)

       a. When set is applied, Q = 1.
       b. When set is not applied and clock is applied, Q = 0. Q value becomes unpredictable
       c. Q cannot be set_bar, because:
           i. When set goes zero, Q does not follow the data
           ii. It will wait for the next clock edge data of D, then Q goes to zero and creates a clock cycle zero as it is in sync with clock
         ![image](https://github.com/user-attachments/assets/5445036d-0061-454d-8d81-f16e3e836698)

       d. For a flop to become sequential constant it needs to be retained

  5. Other concepts like state opt, cloning, retiming

### Unused sequential opt
  1. As the counter goes on, the unused bits in the design which were not connected to primary output, has been optimized. There could be more than one outputs which are unused
  2. For the count having 3 bits, 3 DFFs are used
  3. Now the output Q = count[2].count[1]_bar.count[0]_bar
     ![image](https://github.com/user-attachments/assets/816c60f5-e120-4b1f-a456-455ddd58a5eb)
  
  4. In the previous sequential opt, only count[0] was used and other bits were not used. Synthesis tool will optimize it completely.
  5. All the other logics are visible now because the count bit increased, so to optimize it required additional gates for the final opt

     ![image](https://github.com/user-attachments/assets/1a8bfbb6-4bf3-489d-b51c-00b71c4d4267)



# DAY 4: Gate Level, blocking vs non-blocking and Synthesis simulation mismatch

## Gate Level Simulation

![image](https://github.com/user-attachments/assets/982a6f87-5806-481c-a4ac-b8a5cd4b0401)

  1. Running test bench with netlist as Design Under Test. Originally, RTL netlist was the DUT.
  2. Logically it is the same and will also align with the TestBench
  3. This is to verify logical correctness of design after synthesis and ensure timing of the design is met (GLS needs to be run with delay annotation)
  4. Gate level verilog models will consist of the standard cell defined in them already as we have synthesized it and validate the functionality

```
NOTE: Delay annotation: Gate Level Verilog Models has to be timing aware for correct simulation and output
```

## Synthesis Simulation mismatch

### Missing Senstivity List
  1. In verilog code, the simualtor works based on the activity. i.e, output will change only when the input changes
  2. Ex: For a select pin change with always@(sel), if input is 0, y -> i0 and vice versa.
  3. The always part is not dependent on the input data, so only when there is a change in select data, the always block will get evaluated
  4. Now when always@(*) is given, the always will be evaluated in any signal change (i.e. inputs or sel)
  5. When synthsiszed, it will not check the sensitivity and do only the functionality and will create MUX
  6. So we will have mismatch for this


## Blocking and non-blocking statements in verilog

### Blocking (=)
  1. Executes statements in the order that it is written
  2. So the first statement is evaluated before the second statement

### Non-blocking (<=)
  1. Executes all the RHS when always block is entered and assignes to LHS
  2. Does parallel evaluation for multiple assignments. Ex: a<= b&c; and others, it will do the calculation and then assign the final value
  3. Order of statement execution does not matter

### Caveats with Blocking Statements
#### Ex: Create shift register
  
  ![image](https://github.com/user-attachments/assets/71693d55-37fb-4b49-9198-d23ca635525e)
    
    1. IN the first if loop, the q and q0 is assigned to 0 , i.e. reset
    2. In the else loop, q assigned to q0 and q0 assigned to d
    3. Here, q has the value of q0, only then q0 will have d
    4. By the time, q0 is assigned to d, it already has the value of d and is using only 1 flop
    
#### Ex: Incase the assignment order is changed
  
  ![image](https://github.com/user-attachments/assets/857d52f2-e74c-4eb8-b3bb-2533cadfffc7)
    
    1. Here d is already assigned to q0 and then q0 is assigned to q, the q0 already has data of d

```
NOTE: Use non-blocking for writing sequential circuits
```

#### Ex: Synth Simulation mismatch
   ![image](https://github.com/user-attachments/assets/84dfb5ac-86e6-4bbb-b325-46fe907f12dc)

    1. Using blocking statement, assigning y to q0 and c and then q0 assigned to a|b.
    2. Only when always is executed, the q0 value is updated, or else it is taking the old value
    3. This will mimic a delay or flop
    When this is synthesiszed, there will ne no flop
    4. Now if order is changed
   ![image](https://github.com/user-attachments/assets/21cb4bf5-cbec-4022-b17e-96c6120e3d7d)
       
       a. q0 is evaluated first when always entered
       b. Now for y assigning, latest value of q0 is used in simulation
       c. Now if synthesized, it will do the same circuit as the ORANF gate
    
    5. Because of this mismtach of these issues, we need to run the GLS



# DAY 5: Optimization in synthesis

## If Case constructs 

### If Statement

![image](https://github.com/user-attachments/assets/c6799787-9cab-4e6b-9b8a-db537932a112)

  1. If is used for priority logic
  2. Will consist of begin and end statements
  3. Hardware design will be based on the condition of the loop. It will act mostly like a MUX but with multiple conditions connected to the original input signal to pass through

#### Cautions for If

![image](https://github.com/user-attachments/assets/de6cf8c2-51df-434d-99f5-f7081810e891)

  1. If we get "Inferred Latches"
  2. This has incomplete if statement with no final else code. Using only if and if else only
  3. The latch will store the value and will be driven to the input again
  4. This is a combinational circuit and this behaviour is not acceptable

#### Counter

![image](https://github.com/user-attachments/assets/312be6ed-1d2a-4820-a9ba-24182c884337)

  1. Will include a always block
  2. When the "en" condition is fulfilled, then count is increased by 1
  3. If no "en" count is available, it will latch on to the previous value
  4. This is a intended behaviour in sequential circuit

### Case Statement

![image](https://github.com/user-attachments/assets/f02aab49-745b-48a5-88df-d050027da61c)

  1. Any value being assigned should be a register variable only
  2. Will include a always block to evaluate all the inputs and contain begin and end and end with 'endcase'
  3. It acts like a MUX

#### Cautions for Case
##### Incomplete Case
  
  ![image](https://github.com/user-attachments/assets/4872a042-1484-4f4f-841e-2b363d47d0fc)

  1. Incomplete cases can cause Inferred latches
  2. For 2-bit select condition, if switch is provided for only 2 bits only, then the rest inputs will need to be assigned with default case
  3. With default case we avoid inferred latches

##### Partial assignments in Case
  ![image](https://github.com/user-attachments/assets/7e101ba7-f59f-4020-b0d8-63e381935227)

  1. When sel is 0, x = a & y = b; when sel is 1, x = c, but no y assigned in the case statement
  2. Always assign all the outputs in all the segments of case

### Comparison of If and Case
  1. In If, priority is defined by if, else if and else. Only one can be executed
  2. But in case for each variable value, if MSB is given and LSB is not defined, it will go to unpredictable output. And code is executed from top to bottom flow by checking conditions of each case. Should not have overlapping cases


## Looping constructs
  1. As complexity increases with bit increase and the level of logic increases, it gets difficult to write with normal statement being assigned to each and every data bit
  2. For data to be read faster and efficiently, loops are the best way to execute
     
### For Loop
  1. Inside for loop
  2. Used for evaluating expressions and not for instantiating hardware
  3. We can do this for 256 bit as well, just need to change the last read bit

```ruby
  interger i
    always@(*)
    begin
      for (i=0; i<32; i=i+1)
        begin if (i==sel)
          y=inp[i];
        end
    end
```

Ex: Instantiate DEMUX for 1x8
```ruby
interger i;
always@(*)
  begin
    op_bus[7:0]=8'b0;
    for(i=0; i<8; i=i+1)
      begin
        if(i==sel)
          op_bus[i]=input
      end
  end
```

### Generate for loop
  1. Cannot be used inside always block and should be used outside it
  2. Used for instantiating hardware and replicating the hardware

Ex: Instantiate 8 AND gates

![image](https://github.com/user-attachments/assets/c099ddb3-a5b7-4076-916e-aaa7d71d28a8)

```ruby
  genvar i;
    generate
      for(i=0;i<8;i=i+1)begin
        and u_and (.a(in1[i]), .b(in2[i]), .y(y[i]));
      end
    endgenerate
```

Ex: Ripple carry adder (Multiple Full Adder which gives carry and sum)
  
![image](https://github.com/user-attachments/assets/e8410c41-86c3-4b23-963e-d60d5214a79d)


  
