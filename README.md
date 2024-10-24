# ASIC DESIGN CLASS

### Tools used
- **Software Tools:**
  - GCC (GNU Compiler Collection)
  - RISC-V GNU Compiler Toolchain
  - Spike RISC-V Simulator
  - Ubuntu OS 

<details>
<summary> Assignment 1</summary>
<br>


### Write a C Program and compile it using the GCC compiler to get Output O0 

### * Step 1:- Download leafpad editor in the terminal by using the sudo apt command.

![Leafpad](https://github.com/user-attachments/assets/86e220c4-b8d2-4ce3-94fa-ff5ad14fa29a)
### * Step 2:- Open a new file in the leafpad editor and write the desired c program and save it
### * Step 3:- After saving the file compile it using the GCC Compiler
### * Step 4:- Print the output of the code O0.
<br>

![Output](https://github.com/user-attachments/assets/2d5398da-343b-4974-b09c-a4e1896a1202)

<br>

![sum1ton](https://github.com/user-attachments/assets/d3fb1189-f3db-4bbf-9fe3-8bbacbcfca09)
</details>


<details>
<summary> Assignment 2</summary>
<br>

### To compile and verify the c code on the riscv compiler and verifying the number of lines in the assembly language code manually

### Materials and Tools
  - GCC (GNU Compiler Collection)
  - RISC-V GNU Compiler Toolchain
  - Ubuntu OS

### Step 1:- Compiling the c code on the RISCV compiler

```c
#include<stdio.h>
int main()
{
int i,sum=0,n=57;
for(i=0;i<=n;i++)
{
sum+=i;
}
printf("The Sum of the numbers from 1 to %d is %d ",n ,sum);
return 0;
}
```

### Output:-

```plaintext
THe output of the code is 1653
```

## Screenshots of the compiled result 

![riscv gcc 01](https://github.com/user-attachments/assets/8d413890-5c3a-4883-a5d5-2a61c52349b4)

![riscv gcc ofast](https://github.com/user-attachments/assets/2c7477dc-4667-434a-9ef0-8624b6362f36)

### Step 2:- Get the assembly language code for the given c file

### Once we get the assembly language code we then verify the number of addresses in the code by subtracting the address next to the last line of the code with the first address and dividing the same by 4 since 4 bytes of data is used by each address line

![assembly code riscv gcc 01](https://github.com/user-attachments/assets/174a462f-eabc-4b51-abc1-e898e7c0a3ae)

![assembly code riscv gcc ofast](https://github.com/user-attachments/assets/9e6b5fe8-f404-4e4f-a537-656358699061)

</details>

<details>
<summary> Assignment 3</summary>
<br>
  
## Assignment 3
### Task 1:- 
To find the output of the C program on the RISC V Compiler using the Spike command and debug the code

### In assignment 1 we have compiled and found the output of the c code using the GCC compiler and have found the sum of the n numbers. In assignment 2 we have looked at the assembly code for the same using the objdump command on the RISC V compiler. In assignment 3 we are going to have find the result of the n numbers on the RISCV compiler using the SPIKE command

## Code for compiling the objdump file
```bash
spike pk sum1ton.o
```
### The compiled code using SPIKE command
![result from gcc compiler](https://github.com/user-attachments/assets/4184bd6a-8bc4-40ba-bc97-4c040b7c960a)

### The assembly code of O1
![assembly code](https://github.com/user-attachments/assets/5dc5673f-202b-4896-875c-78242dfb6dac)

### The assembly code of Ofast
![assembly code_ ofast](https://github.com/user-attachments/assets/c743439b-7dea-4e59-86fa-76a79cd51bd5)



## Code for debugging the assembly code obtained in assignment 2
```bash
spike -d pk sum1ton.o
```
### From the assembly code we can see that the first address is at 10184. In order to debug the code we need the program counter to point at this address location. Therefore we use the following command to place the program counter on the the location 10184.

```bash
until pc 0 10184
```
###Similarly we can apply the same logic for Ofast code

```bash
until pc 0 100bo
```

### The first instruction involves the stack pointer. Therefore in order to check the initial and final contents of the stack pointer we use the following code. [O1]

```bash
reg 0 sp
```
### The following are the initial contents of the stack pointer

![stack pointer contents](https://github.com/user-attachments/assets/15734fb6-4390-4a8a-8c46-3d208c517225)
### In the assembly code we can see that the value of the stack pointer is being reduced by 10 in hexadecimal we is equivalent to being reduced by 16 in decimal notation

### After running the first line of the code the contents of the stack pointer get modified and we get the follwoing result

![modified sp](https://github.com/user-attachments/assets/03f6cb0c-2d06-42e1-a38c-36c63a921e6b)

### Similarly for the register a0 we observe the following initial and final contents [ O-fast]

```bash
reg 0 a0
```

![a0 initial contents](https://github.com/user-attachments/assets/2156c1c6-da00-4a39-8b49-b66eab93d527)

### Similarly we can do the same for all the other instructions in the code and find out the contents in the respective addressing locations and their updated values once we execute the lines in the debugger.

</details>

<details>
<summary> Assignment 4 </summary>
<br>

# Task 1:-
RISC-V, a popular open-source instruction set architecture (ISA), employs six basic instruction formats to encode various operations. These formats are designed for efficiency and flexibility. They are as follows:-

## Overview of the RISK V architecture:-
![Risc v architecture](https://github.com/user-attachments/assets/0886862c-554e-44b2-9cd3-80d553964f96)


- ###  R-Type (Register)
  Purpose: Used for arithmetic and logical operations.
  - Format:
    - opcode: 7 bits
    - rd (destination register): 5 bits
    - funct3: 3 bits
    - rs1 (source register 1): 5 bits
    - rs2 (source register 2): 5 bits
    - funct7: 7 bits

- ###  I-Type (Immediate)
  Purpose: Used for immediate arithmetic operations, load instructions, and certain system instructions.

  - Format:  
    - opcode: 7 bits
    - rd (destination register): 5 bits
    - funct3: 3 bits
    - rs1 (source register): 5 bits
    - immediate: 12 bits

- ### S-Type (Store)
  Purpose: Used for store instructions.

  - Format:  
    - opcode: 7 bits
    - immediate[11:5]: 7 bits
    - funct3: 3 bits
    - rs1 (source register 1): 5 bits
    - rs2 (source register 2): 5 bits
    - immediate[4:0]: 5 bits
    
- ### B-Type (Branch)
  Purpose: Used for branch instructions.

  - Format:
  
    - opcode: 7 bits
    - immediate[12]: 1 bit
    - immediate[10:5]: 6 bits
    - funct3: 3 bits
    - rs1 (source register 1): 5 bits
    - rs2 (source register 2): 5 bits
    - immediate[4:1]: 4 bits
    - immediate[11]: 1 bit

- ### U-Type (Upper Immediate)
  Purpose: Used for instructions that need a large immediate value (e.g., LUI).

  - Format:
  
    - opcode: 7 bits
    - rd (destination register): 5 bits
    - immediate: 20 bits

- ### J-Type (Jump)
  Purpose: Used for jump instructions (e.g., JAL).

  - Format:
  
    - opcode: 7 bits
    - rd (destination register): 5 bits
    - immediate[20]: 1 bit
    - immediate[10:1]: 10 bits
    - immediate[11]: 1 bit
    - immediate[19:12]: 8 bits
   
### Here are the RISC-V instructions categorized into their respective types and the corresponding 32-bit instruction codes:

- R-type Instructions:

  - ADD r10, r11, r12
    
    | funct7 | rs2  | rs1  | funct3 | rd   | opcode |
    |--------|------|------|--------|------|--------|
    | 0000000| 01100| 01011| 000    | 01010| 0110011|

  - SUB r12, r10, r11:
    
     |funct7 | rs2  | rs1  | funct3 | rd   | opcode |
     |-------|------|------|--------|------|--------|
     |0100000| 01011| 01010| 000    | 01100| 0110011|

  - AND r11, r10, r12
  
     |funct7 | rs2  | rs1  | funct3 | rd   | opcode |
     |-------|------|------|--------|------|--------|
     |0000000| 01100| 01010| 111    | 01011| 0110011|
  
  - OR r8, r11, r5
  
     |funct7 | rs2  | rs1  | funct3 | rd   | opcode |
     |-------|------|------|--------|------|--------|
     |0000000| 00101| 01011| 110    | 01000| 0110011|
  
  - XOR r8, r10, r4
  
     |funct7 | rs2  | rs1  | funct3 | rd   | opcode |
     |-------|------|------|--------|------|--------|
     |0000000| 00100| 01010| 100    | 01000| 0110011|
  
  - SLT r00, r1, r4
  
    |funct7 | rs2  | rs1  | funct3 | rd   | opcode |
    |-------|------|------|--------|------|--------|
    |0000000| 00100| 00001| 010    | 00000| 0110011|
  
  - SRL r06, r01, r1
  
    |funct7 | rs2  | rs1  | funct3 | rd   | opcode |
    |-------|------|------|--------|------|--------|
    |0000000| 00001| 00001| 101    | 00110| 0110011|

  - SLL r05, r01, r1
 
    |funct7 | rs2  | rs1  | funct3 | rd   | opcode |
    |-------|------|------|--------|------|--------|
    |0000000| 00001| 00001| 001    | 00101| 0110011|

- I-type Instructions:

  - ADDI r02, r2, 5
    |imm    | rs1  | funct3 | rd   | opcode|
    |-------|------|--------|------|-------|
    |000000000101| 00010| 000    | 00010| 0010011|

  - LW r03, r01, 2
    |imm    | rs1  | funct3 | rd   | opcode |
    |-------|------|--------|------|--------|
    |000000000010| 00001| 010    | 00011| 0000011|

- S-type Instructions
   - SW r2, r0, 4

     |imm[11:5]| rs2  | rs1  | funct3 | imm[4:0] | opcode|
     |---------|------|------|--------|----------|-------|
     |0000000 | 00010| 00000| 010    | 00100    | 0100011|

- B-type Instructions
   - BNE r0, r0, 20
     
     |imm[12/10:5]| rs2  | rs1  | funct3 | imm[4:1/11] | opcode |
     |------------|------|------|--------|-------------|------- |
     |0000010     | 00000| 00000| 001    | 01000       | 1100011|

   - BEQ r0, r0, 15
 
     |imm[12/10:5]| rs2  | rs1  | funct3 | imm[4:1/11] | opcode |
     |------------|------|------|--------|-------------|--------|
     |0000011     | 00000| 00000| 000    | 01110       | 1100011|














   

## The final table for the instructions is as follows:-

| Assembly Instruction | Instruction format         |  Hexadecimal equivalent                             | Binary equivalent                      |
|----------------------|----------------------------|-----------------------------------------------------|----------------------------------------|
| ADD r10, r11, r12    | R                          | <code style="color : name_color"> 0x00C58533 </code>| 0000 0000 1100 0101 1000 0101 0011 0011|
| SUB r12, r10, r11    | R                          | <code style="color : name_color"> 0x40B50633 </code>| 0100 0000 1011 0101 0000 0110 0011 0011|
| AND r11, r10, r12    | R                          | <code style="color : name_color"> 0x00C575B3 </code>| 0000 0000 1100 0101 0111 0101 1011 0011|
| OR r8, r11, r5       | R                          | <code style="color : name_color"> 0x0055E433 </code>| 0000 0000 0101 0101 1110 0100 0011 0011|
| XOR r8, r10, r4      | R                          | <code style="color : name_color"> 0x00454433 </code>| 0000 0000 0100 0101 0100 0100 0011 0011|
| SLT r00, r1, r4      | R                          | <code style="color : name_color"> 0x0040A033 </code>| 0000 0000 0100 0000 1010 0000 0011 0011|
| ADDI r02, r2, 5      | I                          | <code style="color : name_color"> 0x00510113 </code>| 0000 0000 0101 0001 0000 0001 0001 0011|
| SW r2, r0, 4         | S                          | <code style="color : name_color"> 0x00202123 </code>| 0000 0000 0010 0000 0010 0001 0010 0011|
| SRL r06, r01, r1     | R                          | <code style="color : name_color"> 0x0010D333 </code>| 0000 0000 0001 0000 1101 0011 0011 0011|
| BNE r0, r0, 20       | B                          | <code style="color : name_color"> 0x00001063 </code>| 0000 0000 0000 0000 0001 0000 0110 0011|
| BEQ r0, r0, 15       | B                          | <code style="color : name_color"> 0x00000063 </code>| 0000 0000 0000 0000 0000 0000 0110 0011|
| LW r03, r01, 2       | I                          | <code style="color : name_color"> 0x0020A183 </code>| 0000 0000 0010 0000 1010 0001 1000 0011|
| SLL r05, r01, r1     | R                          | <code style="color : name_color"> 0x001092B3 </code>| 0000 0000 0001 0000 1001 0010 1011 0011|
 

# Task 2:-

### 

| Assembly Instruction | Instruction format         | Hardcoded ISA  | 
|----------------------|----------------------------|----------------|
| add r6,r1,r2         | R                          | 32'h02208300   |
| sub r7,r1,r2         | R                          | 32'h02209380   |
| and r8,r1,r3         | R                          | 32'h0230a400   |
| or r9,r2,r5          | R                          | 32'h02513480   |
| xor r10,r1,r4        | R                          | 32'h0240c500   |
| slt r11,r2,r4        | R                          | 32'h02415580   |
| addi r12,r4,5        | I                          | 32'h00520600   |
| sw r3,r1,2           | S                          | 32'h00209181   |
| lw r13,r1,2          | I                          | 32'h00208681   |
| beq r0,r0,15         | B                          | 32'h00f00002   |
| add r14,r2,r2        | R                          | 32'h00210700   |



### The waveforms for the original verilog code

``` Add r6,r1,r2 ```

![image](https://github.com/user-attachments/assets/b1e4501e-bd3b-4aaf-9b62-2d5644666cd4)

``` Sub r7,r1,r2 ```

![image](https://github.com/user-attachments/assets/24c3f1f0-91f1-4bcd-96c5-f82de03b4362)

``` And r8,r1,r3 ```

![image](https://github.com/user-attachments/assets/510fbd69-a0a1-4730-9586-b8c12cb995ea)

``` Or r9,r2,r5 ```

![image](https://github.com/user-attachments/assets/d4684ab4-fc66-4811-817b-8431691f41bf)

``` Xor r10,r1,r4 ```

![image](https://github.com/user-attachments/assets/7f9a3c78-af51-417b-a031-5cd63b02a3a7)

``` slt r11,r2,r4 ```

![image](https://github.com/user-attachments/assets/e65c85b2-f9d8-4687-b9d2-23bc5044a3dd)

``` addi r12,r4,5 ```

![image](https://github.com/user-attachments/assets/ce8a622a-a6e3-4192-8858-e9185d35bd59)

``` sw r3,r1,2 ```

![image](https://github.com/user-attachments/assets/a9f28035-1d60-41b0-a418-2a5d7882d972)

``` lw r13,r1,2 ```

![image](https://github.com/user-attachments/assets/7afdd0e9-3d75-4125-9131-0d2146e8aeba)

``` beq r0,r0,15  ```

![image](https://github.com/user-attachments/assets/4f067a51-a211-4726-a457-0e567ca0406b)

``` add r14,r2,r2 ```

![Og_11](https://github.com/user-attachments/assets/3f3fce3a-581a-4b15-8a9b-0f880ffb8e52)


### The waveforms according to the instructions assignmed to me


```  ADD r10, r11, r12 ```

![image](https://github.com/user-attachments/assets/e1587db3-9081-43e5-8f0f-7b909a7557a5)

``` SUB r12, r10, r11 ```

![image](https://github.com/user-attachments/assets/c16aa95a-c37f-47cd-8335-04c24a40cd54)

``` AND r11, r10, r12 ```

![image](https://github.com/user-attachments/assets/d32083c5-8b8f-4979-9d58-ba4a2f87932e)

``` OR r8, r11, r5 ```

![image](https://github.com/user-attachments/assets/0b9aa44e-8cef-47cb-a7b2-c92fa1a507c0)

``` XOR r8, r10, r4 ```

![image](https://github.com/user-attachments/assets/e9057d8e-4ff1-4d8d-bf51-5ec59b8af948)

``` SLT r00, r1, r4 ```

![image](https://github.com/user-attachments/assets/54242fff-2179-48f5-b91b-ed2e21e1a5e3)

``` ADDI r02, r2, 5 ```

![image](https://github.com/user-attachments/assets/168a6af1-d8c1-403e-8427-67811bc4fbca)

``` SW r2, r0, 4 ```

![My_code_8](https://github.com/user-attachments/assets/58363200-d22e-4f73-9039-480695a03adc)

``` SRL r06, r01, r1 ```

![image](https://github.com/user-attachments/assets/888422ca-e4bb-42bd-91af-094fca1d5394)

``` BNE r0, r0, 20 ```

![image](https://github.com/user-attachments/assets/a4efe01c-1dd0-46d3-9847-f7c19b51ae31)

``` BEQ r0, r0, 15 ```

![image](https://github.com/user-attachments/assets/131bd04f-e3db-4584-804d-31eab57f0496)

``` LW r03, r01, 2 ```

![image](https://github.com/user-attachments/assets/1966c656-6916-4486-b864-8731421cc0b0)

``` SLL r05, r01, r1 ```

![image](https://github.com/user-attachments/assets/55578f7c-275b-42e4-b7d4-b91c2de8f741)


## Conclusion

The ISA used by us is not in accordance with the one which is used in the program. Therefore we can observe some discrepancies in the outputs of the instructions assigned to me and the original instructions which were designed with respect to a different ISA.

</details>

<details>
<summary> Assignment 5</summary>
<br>

## Write a code for an Analog Comparator in C to compare the analog voltages

### * Step 1:- Open the leafpad editor and write the c code which is executable on gcc and risc v gcc

```bash
#include <stdio.h>

// Mock function to simulate analog read
int analogRead(int pin) {
    // In real application, this would interface with hardware ADC
    return pin * 100;  // Example value
}

int main() {
    int pinA = 3;
    int pinB = 4;
    int valueA, valueB;

    // Read analog inputs
    valueA = analogRead(pinA);
    valueB = analogRead(pinB);

    // Compare values
    if (valueA > valueB) {
        printf("Pin A has a higher voltage.\n");
    } else if (valueA < valueB) {
        printf("Pin B has a higher voltage.\n");
    } else {
        printf("Both pins have the same voltage.\n");
    }

    return 0;
}
```


![gcc image 1](https://github.com/user-attachments/assets/318f4caf-6613-4bbe-b240-06e800ce4f6a)

### * Step 2:- Compile the above code using this command on the gcc compiler. 
```bash
gcc analogcomp.c
```
Here analogcomp is the name of my c program file

### * The output of the code is as follows:-

![gcc image 2](https://github.com/user-attachments/assets/a6624c2b-8f71-458c-a35c-7c5980d18f3e)

### * Step 3:- Compile the above code on RISC V architecture for O1 and Ofast 

### For O1
 We run the following  command in order to compile the c code on risc v architecture for O1
```bash
riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o analogcomp.o analogcomp.c
```
 The output is as follows

![O1_output](https://github.com/user-attachments/assets/8e7f425a-eca4-4345-be0b-eaa863f3237b)

 We are only concerned with the corresponding assembly language program out of the output generated previously. In order to get the same we run the following code.

```bash
riscv64-unknown-elf-objdump -d analogcomp.o | less
```

The output is as follows and the number of instructions in the assembly code can be found out as follows:-

![main_function riscv o1](https://github.com/user-attachments/assets/e14675c1-3f2e-4b5f-8efa-cfcbe255e138)

Here we can observe that the decimal value is 180. Also in the assembly language 1 line of code takes up 4 bytes of space in the memory therefore we can verify that the number of lines in the assembly language is 180/4 which is 45.

### For Ofast

We run the following  command in order to compile the c code on risc v architecture for O-fast
```bash
riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o analogcomp.o analogcomp.c
```
 The output is as follows
![ofast_output](https://github.com/user-attachments/assets/d8edebb7-752c-4e60-831c-4a3892fcca8e)


 We are only concerned with the corresponding assembly language program out of the output generated previously. In order to get the same we run the following code.
 
```bash
riscv64-unknown-elf-objdump -d analogcomp.o | less
```

The output is as follows and the number of instructions in the assembly code can be found out as follows:-

![ofast output_new](https://github.com/user-attachments/assets/c0b098b3-f176-4a9b-b840-1b2e1de52e06)

Similar to O1 we can see that the decimal value of obtained is 36 which when divided by 4 gives us 9 which are the total number of addressing lines in our code.

### Result of the RISC V O1 and Ofast command

Code for compiling the objdump file
```bash
spike pk analogcomp.o
```

Result for O1

![Spike O1](https://github.com/user-attachments/assets/4ca600a6-10ed-4f2d-b5f3-2974dc064a94)

Result for Ofast

![Spike Ofast](https://github.com/user-attachments/assets/59dea6da-dccd-4713-b6e4-ad34c59a3826)

### Debegging the assembly code for O1 and Ofast

We use the following command for debugging the code

```bash
spike -d pk analogcomp.o
```
For O1 we have the following code

![debugger_o1](https://github.com/user-attachments/assets/550d7cbc-11a2-4440-abd0-216e5f5a9d09)

For Ofast we have the following code

![debugger_ofast](https://github.com/user-attachments/assets/5aa1081e-f8e7-439a-8792-b2becbc8ebc1)

While debugging we have found out the starting address and have initialised the program counter to this address. The first instruction for both O1 and Ofast involves the stack pointer so we have found out the starting address of the stack pointer. After the execution of that instruction we can observe that the address of the stack pointer is to be reduced by 32 in hexadecimal which is equivalent to 20 in decimal which is what we observe when the address of the stack pointer reduces from 50 to 30. Similarly we can do the same for the rest of the instructions.

### Conclusion

We have thereby verified the output of the analog comparator on the GCC and the RISC V GCC compilera and debugged the output using the spike command for both O1 and Ofast.


</details>



</details>

<details>
<summary> Assignment 6</summary>
<br>
	
# Digital Logic with TL-Verilog and Makerchip

### Sequential Calculator

Calculators tend to remember the previous result and use it for the next operation. The sequential calculator does this and feeds back the output to the next input. The code for the same is as follows:-

```bash
\m5_TLV_version 1d: tl-x.org
\m5
   
   // =================================================
   // Welcome!  New to Makerchip? Try the "Learn" menu.
   // =================================================
   
   //use(m5-1.0)   /// uncomment to use M5 macro library.
\SV
   // Macro providing required top-level module definition, random
   // stimulus support, and Verilator config.
   m5_makerchip_module   // (Expanded in Nav-TLV pane.)
	
\TLV
   //$count[31:0] = 32'b0;
   
   // Sequential Clock
   
   |calc
      @1
         $clk_omkar = *clk;
         $reset = *reset;
         $val1[31:0] = >>1$result[31:0];
         $val2[31:0] = $rand2[3:0];
         $result[31:0] = $reset ? 32'b0 : ($sel[1:0] == 2'b00)
                         ? ($val1[31:0] + $val2[31:0]) : ($sel[1:0] == 2'b01)
                         ? ($val1[31:0] - $val2[31:0]) : ($sel[1:0] == 2'b10)
                         ? ($val1[31:0] * $val2[31:0]) : ($sel[1:0] == 2'b11)
                         ? ($val2[31:0] != 0 ? ($val1[31:0] / $val2[31:0]) : 32'bx) :  32'b0;
         //$count[31:0] = $reset  ? 0 : (>>1$count + 1);
   
   // Assert these to end simulation (before Makerchip cycle limit).
   *passed = *cyc_cnt > 40;
   *failed = 1'b0;
\SV
	endmodule;

```

This gives us the following waveforms and block diagram:-

![image](https://github.com/user-attachments/assets/55434301-1098-4344-ae9f-2246f605a276)

### Pipelined Logic:-

Pipelining is used to maximise resource utilisation and thus reduce the delays in performing all the operations in a given task. In order to do so me make sure that every block in our system is working almost in every cycle such that it does not affect the operation of any other block which may be dependent or independent of its result. We have used a pythagorean calculator in our case. The code for the same is as follows.

```bash
\m5_TLV_version 1d: tl-x.org
\m5
   // =================================================
   // Welcome!  New to Makerchip? Try the "Learn" menu.
   // =================================================
   
   //use(m5-1.0)   /// uncomment to use M5 macro library.
\SV
	`include "sqrt32.v"
   // Macro providing required top-level module definition, random
   // stimulus support, and Verilator config.
   m5_makerchip_module   // (Expanded in Nav-TLV pane.)
\TLV
   |calc
      @1
         $reset = *reset;
         $clk_omkar = *clk;
      ?$valid
         @1
            $aa_sq[31:0] = $aa[3:0] * $aa[3:0];
            $bb_sq[31:0] = $bb[3:0] * $bb[3:0];
         @2
            $cc_sq[31:0] = $aa_sq + $bb_sq;
         @3
            $cc[31:0] = sqrt($cc_sq);
         //@4
         //$tot_dist[63:0] = $reset ? 0 : $valid ? (>>1$tot_dist + $cc) : >>1$tot_dist;
            
         //@4
         //$adder[31:0] = $cc + >>1$tot_dist;
         //@5
         //$tot_dist[31:0] = $valid ? ( >>1$tot_dist + $adder ) : >>1$tot_dist
   
   // Assert these to end simulation (before Makerchip cycle limit).
   *passed = *cyc_cnt > 16'd30;
   *failed = 1'b0;
\SV
   endmodule
```

The output for the following code is as follows:-

![Pipelined_logic](https://github.com/user-attachments/assets/291685cf-eb23-46ea-a894-68b6faf91deb)

### Cycle Calculator

In the sequential calculator we have taken the output of the previous result and fed it back to the next input but in this case we are using 3 stages of pipeline instead of 2 and therefore the calculator input will receive input which is 2 cycles older.

```bash

\m5_TLV_version 1d: tl-x.org
\m5
   
   // =================================================
   // Welcome!  New to Makerchip? Try the "Learn" menu.
   // =================================================
   
   //use(m5-1.0)   /// uncomment to use M5 macro library.
\SV
   // Macro providing required top-level module definition, random
   // stimulus support, and Verilator config.
   m5_makerchip_module   // (Expanded in Nav-TLV pane.)
\TLV
   //$count[31:0] = 32'b0;
   |calc
      @1
         $clk_omkar = *clk;
         $reset = *reset;
         $val1[31:0] = >>2$result[31:0];
         $val2[31:0] = $rand2[3:0];
         
      @2
         $valid = $reset ? 0 : (>>1$valid + 1);
         $out[31:0] = ($reset | !($valid)) ? 32'b0 : ($sel[1:0] == 2'b00) ? ($val1[31:0] + $val2[31:0]) : ($sel[1:0] == 2'b01) ? ($val1[31:0] - $val2[31:0]) : ($sel[1:0] == 2'b10) ? ($val1[31:0] * $val2[31:0]) : ($sel[1:0] == 2'b11) ? ($val2[31:0] != 0 ? ($val1[31:0] / $val2[31:0]) : 32'bx) :  32'b0;
         
   
   // Assert these to end simulation (before Makerchip cycle limit).
   *passed = *cyc_cnt > 40;
   *failed = 1'b0;
\SV
   endmodule

```

The output for the cycle calculator is as follows:-

![Cycle_calculator](https://github.com/user-attachments/assets/264f1c05-9198-4440-b2ec-fbf17d0d14ca)

### Validity

When we generate a waveform as in all the previous cases we are receiving a result for all the clock cycles. Here there are no compilation errors but it is quite possible that logical errors can be present in these cases. These errors will be ignored during compile time and it will be difficult to debug them by simply looking at the waveforms. Also there might be certain cases where a dont care condition comes up. These cases are insignificant to us and thus should be neglected . In order to do so we use the Validity. The global clock is also running all the time. There might be instances in our code when we do not need a particular case to run but still does as the clock triggers it. In order to execute a clock physically voltage or current sources are used. These sources use some power during that clock cycle. In complex circuits if such cases are ignored a lot of power will be wasted. So in order to reduce power consumption we remove the clock during such cycles and this process is called as clock gating. The validity helps us with this.

The code for Validity is as follows for the pythagorean calculator:-

```bash
\m5_TLV_version 1d: tl-x.org
\m5
   // =================================================
   // Welcome!  New to Makerchip? Try the "Learn" menu.
   // =================================================
   
   //use(m5-1.0)   /// uncomment to use M5 macro library.
\SV
	`include "sqrt32.v"
   // Macro providing required top-level module definition, random
   // stimulus support, and Verilator config.
   m5_makerchip_module   // (Expanded in Nav-TLV pane.)
\TLV
   |calc
      @1
         $reset = *reset;
         $clk_omkar = *clk;
      ?$valid
         @1
            $aa_sq[31:0] = $aa[3:0] * $aa[3:0];
            $bb_sq[31:0] = $bb[3:0] * $bb[3:0];
         @2
            $cc_sq[31:0] = $aa_sq + $bb_sq;
         @3
            $cc[31:0] = sqrt($cc_sq);
            //@4
            //$tot_dist[63:0] = $reset ? 0 : $valid ? (>>1$tot_dist + $cc) : >>1$tot_dist;
            //@4
            //$adder[31:0] = $cc + >>1$tot_dist;
            //@5
            //$tot_dist[31:0] = $valid ? ( >>1$tot_dist + $adder ) : >>1$tot_dist

   // Assert these to end simulation (before Makerchip cycle limit).
   *passed = *cyc_cnt > 16'd30;
   *failed = 1'b0;
\SV
   endmodule
```

The output for the following code is as follows:-

![validity_pytha](https://github.com/user-attachments/assets/722d8573-052f-461d-9642-d88027b8fa5d)

### Total Distance Calculator

Used to calculate the total distance travelled in a series of hops. The code for the same is given as follows:-

```bash
\m5_TLV_version 1d: tl-x.org
\m5
   // =================================================
   // Welcome!  New to Makerchip? Try the "Learn" menu.
   // =================================================
   
   //use(m5-1.0)   /// uncomment to use M5 macro library.
\SV
	`include "sqrt32.v"
   // Macro providing required top-level module definition, random
   // stimulus support, and Verilator config.
   m5_makerchip_module   // (Expanded in Nav-TLV pane.)
\TLV
   |calc
      @1
         $reset = *reset;
         $clk_omkar = *clk;
      ?$valid
         @1
            $aa_sq[31:0] = $aa[3:0] * $aa[3:0];
            $bb_sq[31:0] = $bb[3:0] * $bb[3:0];
         @2
            $cc_sq[31:0] = $aa_sq + $bb_sq;
         @3
            $cc[31:0] = sqrt($cc_sq);
         @4
            $tot_dist[63:0] = $reset ? 0 : $valid ? (>>1$tot_dist + $cc) : >>1$tot_dist;

   // Assert these to end simulation (before Makerchip cycle limit).
   *passed = *cyc_cnt > 16'd30;
   *failed = 1'b0;
\SV
   endmodule
```
The output for the above code is as follows:-

![Total_distance_calculator](https://github.com/user-attachments/assets/49ba4c3c-893b-40c0-9742-cb75a2b8d182)


### Validity on Cycle Calculator

The code is as follows:-

```bash
\m5_TLV_version 1d: tl-x.org
\m5
   
   // =================================================
   // Welcome!  New to Makerchip? Try the "Learn" menu.
   // =================================================
   
   //use(m5-1.0)   /// uncomment to use M5 macro library.
\SV
   // Macro providing required top-level module definition, random
   // stimulus support, and Verilator config.
   m5_makerchip_module   // (Expanded in Nav-TLV pane.)
\TLV
   //$count[31:0] = 32'b0;
   |calc
      @1
         $clk_omkar = *clk;
         $reset = *reset;
         $valid = $reset ? 0 : (>>1$valid + 1);
         $valid_or_reset = $valid || $reset;
      ?$valid
         @1
            $val1[31:0] = >>2$result[31:0];
            $val2[31:0] = $rand2[3:0];
         @2
            $out[31:0] = $valid_or_reset ? 32'b0 : ($sel[1:0] == 2'b00) ? ($val1[31:0] + $val2[31:0]) : ($sel[1:0] == 2'b01) ? ($val1[31:0] - $val2[31:0]) : ($sel[1:0] == 2'b10) ? ($val1[31:0] * $val2[31:0]) : ($sel[1:0] == 2'b11) ? ($val2[31:0] != 0 ? ($val1[31:0] / $val2[31:0]) : 32'bx) :  32'b0;
   // Assert these to end simulation (before Makerchip cycle limit).
   *passed = *cyc_cnt > 40;
   *failed = 1'b0;
\SV
   endmodule

```

The output is as follows:-

![validity_cycle_calculator](https://github.com/user-attachments/assets/459c4f68-b246-448a-8845-5665fff4f4f8)



# Basic RISC-V CPU microarchitecture

In this step we are designing the individual blocks of the microprocessor.

![image](https://github.com/user-attachments/assets/58c6a3f1-ba27-43a9-aff0-1fa285ff7a73)


  
### Program Counter

The program counter is supposed to increase its value by 4 to fetch the next instruction from the memory. The below image specifies the same. In case a reset is triggered the program counter will be initialised to zero for the next instruction.

The following diagram explains the working of the program counter

![image](https://github.com/user-attachments/assets/72baefa6-30cb-4a22-8caa-b370954765bc)

The following is the code for the working of the program counter

```bash
$pc[31:0] = >>1$reset ? 0 : ( >>1$pc + 31'h4 );
```
We get the following output after executing the code:-

![image](https://github.com/user-attachments/assets/9eef0a38-71d1-4fa4-bbf6-aa98283bc534)


### Adding the instruction memory

The program counter points to the next address where the instruction is present in the instruction memory. We need to fetch this instruction in order to process it and make further calculations.

![image](https://github.com/user-attachments/assets/076a1cc9-81f8-4603-8612-394ddd2078fd)

```bash
$imem_rd_en = >>1$reset ? 0 : 1;
$imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
$instr[31:0] = $imem_rd_data[31:0];
```

The output of the following code is as follows:-

![Instruction_memory](https://github.com/user-attachments/assets/2339469d-dc31-486d-8be6-b943fbaa8a98)


### Decoding the instruction

We have decoded the instruction on the basis of all the 6 types of RISC V instruction set. The code for decoding is as follows:-

```bash
$is_i_instr = $instr[6:2] ==? 5'b0000x ||
              $instr[6:2] ==? 5'b001x0 ||
              $instr[6:2] ==? 5'b11001;
$is_r_instr = $instr[6:2] ==? 5'b01011 ||
              $instr[6:2] ==? 5'b011x0 ||
              $instr[6:2] ==? 5'b10100;
$is_s_instr = $instr[6:2] ==? 5'b0100x;
$is_b_instr = $instr[6:2] ==? 5'b11000;
$is_j_instr = $instr[6:2] ==? 5'b11011;
$is_u_instr = $instr[6:2] ==? 5'b0x101;
```

The output is as follows:-

![image](https://github.com/user-attachments/assets/d3504a8b-d0fc-4575-b5f7-fd0ddc3ca448)


### Immediate Decode Logic

The instruction sets have an immediate field. In order to decoder this field we use the following code:-

```bash
$imm[31:0] = $is_i_instr ? {{21{$instr[31]}}, $instr[30:20]} :
                      $is_s_instr ? {{21{$instr[31]}}, $instr[30:25], $instr[11:7]} :
                      $is_b_instr ? {{20{$instr[31]}}, $instr[7], $instr[30:25], $instr[11:8], 1'b0} :
                      $is_u_instr ? {$instr[31:12], 12'b0} :
                      $is_j_instr ? {{12{$instr[31]}}, $instr[19:12], $instr[20], $instr[30:21], 1'b0} :
                      32'b0;
```

![image](https://github.com/user-attachments/assets/cebd84e6-f460-47ed-a6de-d3eb8f51a6fa)


### Decode logic for other fields

Apart from the immediate we have other fields which also need to be decoded. The code for the same is as follows:-

```bash
$rs2_valid = $is_r_instr || $is_s_instr || $is_b_instr;
         ?$rs2_valid
            $rs2[4:0] = $instr[24:20];
            
         $rs1_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         ?$rs1_valid
            $rs1[4:0] = $instr[19:15];
         
         $funct3_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         ?$funct3_valid
            $funct3[2:0] = $instr[14:12];
            
         $funct7_valid = $is_r_instr ;
         ?$funct7_valid
            $funct7[6:0] = $instr[31:25];
            
         $rd_valid = $is_r_instr || $is_i_instr || $is_u_instr || $is_j_instr;
         ?$rd_valid
            $rd[4:0] = $instr[11:7];
```
At a time only one instruction is passed on to for decode. This instruction can be of any 1 of the 6 instruction set types. Thus we need to validate that it belongs to the respective category or else there may be a clash of different instruction set types.

![image](https://github.com/user-attachments/assets/b0033133-1070-484c-86bd-4931b4eaf296)

### Decoding Individual Instructions

We are decoding the individual instructions using the following code

```bash
$dec_bits [10:0] = {$funct7[5], $funct3, $opcode};
$is_beq = $dec_bits ==? 11'bx_000_1100011;
$is_bne = $dec_bits ==? 11'bx_001_1100011;
$is_blt = $dec_bits ==? 11'bx_100_1100011;
$is_bge = $dec_bits ==? 11'bx_101_1100011;
$is_bltu = $dec_bits ==? 11'bx_110_1100011;
$is_bgeu = $dec_bits ==? 11'bx_111_1100011;
$is_addi = $dec_bits ==? 11'bx_000_0010011;
$is_add = $dec_bits ==? 11'b0_000_0110011;
```
We also have to update the program counter

```bash
$pc[31:0] = >>1$reset ? 32'b0 :
>>1$taken_branch ? >>1$br_target_pc :
>>1$pc + 32'd4;
```

The output for the above code is as follows:-

![image](https://github.com/user-attachments/assets/671e6e35-f9b2-4726-9ed4-3aee6df9e99c)

### Register File Read and Enable

Here we read the instructions from the respective instruction memory and store it in the registers. We have 2 register slots the read the instructions from the memory. We send these stored instructions to the ALU after this process.

The code is as follows:-

```bash
$rf_rd_en1 = $rs1_valid;
$rf_rd_index1[4:0] = $rs1;
$rf_rd_en2 = $rs2_valid;
$rf_rd_index2[4:0] = $rs2;

$src1_value[31:0] = $rf_rd_data1;
$src2_value[31:0] = $rf_rd_data2;
```

The output for the code is as follows:-

![image](https://github.com/user-attachments/assets/28ba722a-4320-4deb-a5a7-8c7ccaceecac)

### Arithmetic and Logic Unit

Used to perform arithmetic operations on the values stored in the registers. The code for the same is as follows:-

```bash
$result[31:0] = $is_addi ? $src1_value + $imm :
                $is_add ? $src1_value + $src2_value :
                32'bx ;
```

Here we have written code for the addi and add operation.

![image](https://github.com/user-attachments/assets/2d40115d-c6d8-4ed0-9006-eb507c3ba415)

### Register File Write

Once the ALU performs the operations on the values stored in ther registers we may need to put these values back into these registers based. For this we use the register file write. We also have to make sure that we should not write into the register if the destination register is x0 as it is always meant to be 0. The code is as follows:-

```bash
$rf_wr_en = $rd_valid && $rd != 5'b0;
$rf_wr_index[4:0] = $rd;
$rf_wr_data[31:0] = $result;
```

![image](https://github.com/user-attachments/assets/a2c1f0d4-0c8f-4400-b81a-c12d0ec20ddd)

### Branch instructions

Based on the control input we may need to jump to some different address after a particular instruction based on some condition generated during run-time. This is when we use the branch instructions. The code is as follows:-

```bash
$taken_branch = $is_beq ? ($src1_value == $src2_value):
	        $is_bne ? ($src1_value != $src2_value):
	        $is_blt ? (($src1_value < $src2_value) ^ ($src1_value[31] != $src2_value[31])):
	        $is_bge ? (($src1_value >= $src2_value) ^ ($src1_value[31] != $src2_value[31])):
                $is_bltu ? ($src1_value < $src2_value):
                $is_bgeu ? ($src1_value >= $src2_value):
	        1'b0;
$br_target_pc[31:0] = $pc +$imm;
```
The output is as follows:-

![image](https://github.com/user-attachments/assets/fbb3a7b5-3b26-4299-b6e0-5ef9b8b335bc)


### Testbench
In order to check whether the code written is correct or not we verify it using the testbench for the 1st five cycles

```bash
*passed = |cpu/xreg[10]>>5$value == (1+2+3+4+5+6+7+8+9) ;
```

Upon checking the log file we get the following result

![image](https://github.com/user-attachments/assets/5602e0c3-ce91-4f02-867c-36d600824fb0)

# Pipelined RISC V CPU
We observe some interdependencies of the values on one another during the execution of the instructions. Thus incorrect data gets processed and we get logical errors in the code. In order to solve these problems we have increased the number of pipelined stages in the code.



Final Pipelined Output:-

We can observe the values in the different registers on the viz tab. The following image shows the 1st clock cycle. 

![image](https://github.com/user-attachments/assets/04a4dd68-11b8-4dda-9d3f-f13f56d1fe31)

Just like the above cycle we can move across different clock cycles and see the updated results in the registers. In our code we are gradually adding the values from 1 to 9 and are observing the final output in the registers. It takes 53 cycles for the register r14 to get updated to the value 45.

![image](https://github.com/user-attachments/assets/d79de8b8-f708-42dd-b099-20182834f413)

The execution of the full code takes 58 cycles including the load and the store operations.

![image](https://github.com/user-attachments/assets/baf7967a-98f1-4ffb-a9d3-378ca56ed3b0)



The following image shows the clock signal which contains my name clk_omkar

![image](https://github.com/user-attachments/assets/21b93a63-758e-4904-bcdd-8a692defff36)

The following image shows the reset signal 

![image](https://github.com/user-attachments/assets/32c6e3f1-99b5-4fd5-bbca-a0ddde1b906c)

The following image shows the gradual addition of the in the r14 register

![image](https://github.com/user-attachments/assets/9ffdb14b-506b-4a7d-ac72-3756731ffd26)


The following is the final block diagram of the processor designed 

![image](https://github.com/user-attachments/assets/f90b3d7e-52f3-4b58-a1a9-534076741a7d)

































</details>

<details>
<summary> Assignment 7</summary>
	
# Convert TLV to Verilog using Sandpiper and write a testbench and simulate using iverilog and gtkwave to view the output waveforms. Plot below signals from gtkwave

Firstly we need to add the sandpiper module and the other necessary packages as follows:-

```bash
 $ sudo apt install make python python3 python3-pip git iverilog gtkwave docker.io
 $ sudo chmod 666 /var/run/docker.sock
 $ cd ~
 $ pip3 install pyyaml click sandpiper-saas
```

After this we need to clone the repo containing VSDBabySoC design files and testbench using the following commands

```bash
git clone https://github.com/manili/VSDBabySoC.git
```

We now need to convert the original TLV file to the verilog code with the help of the sandpiper package.

```bash
sandpiper-saas -i ./src/module/*.tlv -o rvmyth.v --bestsv --noline -p verilog --outdir ./src/module/
```

We now have the verilog code with us. We now need to run this verilog code along with the testbench and get the output using the following command.

```bash
iverilog -o output/pre_synth_sim.out -DPRE_SYNTH_SIM src/module/testbench.v -I src/include -I src/module
```

After this we need to generate the .vcd file which will be executed in the gtkwave platform to create the waveforms.

```bash
./pre_synth_sim.out
```

After creating the .vcd file now we run this file on gtkwave by using the below command 

```bash
gtkwave pre_synth_sim.out
```

I have executed all the above code as follows:-

![image](https://github.com/user-attachments/assets/1b9ed9cb-e517-4b01-982c-72987ae23b37)

Upon executing the gtkwave file We get the following waveform which is the addition of the numbers from 1 to 10

![image](https://github.com/user-attachments/assets/fbcec343-e202-4f40-9c95-560abd6994cc)
	
</details>

<details>

 <summary> Assignment 8</summary>

 # Addition of Peripherals to convert the Digital output to analog output using DAC and PLL

 In this assignment we are adding two peripherals to convert the digital output to the analog output namely PLL and DAC. 
 
 - **Phase locked loop:-** The crystal oscillator present on the board is capable of giving a clock of frequency between 12 - 20 MHZ. The processor operates at frequency near 100MHZ and thus we need an IP/Peripheral to convert this low frequency clock to a high frequency clock. Here the PLL comes into picture. The input to the PLL is the crystal oscillator clock and returns a high frequency clock to our risc v core. This clock is then appended by my name CPU_clk_omkar_a0.
 - **Digital to Analog Converter:-** The processor works with digital input but we transmit or receive signals in analog form. So in order to convert the digital signal in our risc v core to analog signal we are using the digital to analog converter IP.

Commands used to run the rvmyth.v file

```bash
iverilog -o ./pre_synth_sim.out -DPRE_SYNTH_SIM src/module/testbench.v -I src/include -I src/module/
```

After this we dump the ./pre_synth_sim.out file to create the .vcd file using the following command

```bash
./pre_synth_sim.out
```

We then run this .vcd file on gtkwave to observe the output

```bash
gtkwave pre_synth_sim.vcd
```

The above process has been executed by me in the following way

![Screenshot from 2024-08-31 18-24-12](https://github.com/user-attachments/assets/780965ae-5145-4cdc-b61b-9bee7bf055be)




The output of the above code is as follows:-


![Screenshot from 2024-08-31 17-58-40](https://github.com/user-attachments/assets/8f2dc1f8-8e31-4f48-a163-f2109e422d71)


 
</details>









    

 


 







 




 
</details>


<details>


 <summary> Assignment 9 </summary>

 # Introduction to Verilog RTL Design and Synthesis

 ### Simulator

 Tool used to check the RTL Design for gievn specifications. It is iverilog in my case.

 ### Design

 Verilog code or set of verilog code which includes functionality to meet with the required specifications.

 ### Testbench

 Setup to apply stimulus to the design to check the functionality.


 # LAB 1 (Installation of the Repository)

 ![image](https://github.com/user-attachments/assets/076b3284-b040-45c3-b92c-a7d32fbf4482)

 The following picture shows us all the verilog codes and the corresponding testbench files present in the repository.

 ![image](https://github.com/user-attachments/assets/b56df89b-e3a6-4db4-9cda-065a50ca7265)


  # LAB 2(Simulation using Iverilog and Gtkwave)


 ![image](https://github.com/user-attachments/assets/1a10b446-08a9-4644-80c6-41b7a29b1283)

 ![image](https://github.com/user-attachments/assets/91577ff0-3fab-4452-9653-66f28dd9bb0f)

The verilog code and its corresponding testbench as follows:-


 ![image](https://github.com/user-attachments/assets/62da0621-9834-40b7-bfba-a73fa423926a)


### Synthesizer

It is the tool which is used to convert an RTL to a netlist. Yosys is the synthesizer which is used in my case.

![image](https://github.com/user-attachments/assets/3d72d6bd-21e3-4a87-9fec-a847335a3dd3)

Here the Netlist is the representation of the design in the form of the standard cells present in the .lib file.

![image](https://github.com/user-attachments/assets/ae2b4e34-9ff6-4901-b341-16812657d2d9)

### Verification of Synthesis

![image](https://github.com/user-attachments/assets/b5bf62c3-28b5-44ea-90ae-11a7380a46f0)

We use the same testbench which was used for RTL simulation earlier to find the output using gtkwave. We can do this only because the primary inputs fed into the design and that of the netlist will remain the same.

## Logic Synthesis

### RTL Design

It is the behavioural representation of the required specification.

![image](https://github.com/user-attachments/assets/92bb8277-b40f-4d38-a310-21c819304aa3)

So now we have an RTL code but we need to map this code into a circuit which is where we use the process of synthesis. The RTL code is converted into the gates and connections are made between the gates and this is called as netlist.

![image](https://github.com/user-attachments/assets/a60e9806-64f7-43ba-9e77-3bb86c3a22c3)


### What is .lib?

It is a collection of logical modules. It includes basic logic gates like AND,OR, NOT, etc, It contains the different flavours of the same input as in it will have different versions of the same gate. For example in the and gate it will contain a slow,medium and fast version of the AND gate.

### Why do we need different versions of the same gate?

The combinational delay in the circuit is responsible for the maximum speed of operaiton of the digital logic circuit. So we need cells that can work faster to make the combinational delay as small as possible. Thus in this case we need the combinational logic to be as fast as possible so that the required logic can be generated before the arrival of the next clock.

![image](https://github.com/user-attachments/assets/87111b3f-a648-4be2-947f-d518d029b238)

### So why do we need slow cells?

We need slow cells to avoid the hold time violation. We need to capture the logic after the arrival of the clock. For this we need the logic to remain intact for a certain period of time. This is the hold time. If we use faster logic gates then it is possible that we might get a hold time violation.

![image](https://github.com/user-attachments/assets/8ea42c58-5e37-4ffb-9ef3-25bfbb5fe181)

## Faster vs Slower cells

### Faster cells

Advantages:- Less delay.
Disadvatages:- More area and power.

If the width of the transistors will be more it means that they will be able to source more current thereby reducing the delay.

### Slower Cells

Advantages:- Less area and power.
Disadvantages:- More Delay.

Based on the above information we need to use the cells which take care of the above points. So we need to guide the synthesizer through a constraints file.


# Lab 3 ( Introduction to YOSYS)

We have a design in the form of a verilog code which we need to convert into a netlist. For this purpose we are using the synthesizer called YOSYS. In this lab we use the YOSYS synthesizer which uses the components present in the .lib file to make the netlist.

![image](https://github.com/user-attachments/assets/3f1c6dcd-3d17-4ac8-ae91-5d66b296c888)

![image](https://github.com/user-attachments/assets/9f67c0f2-2a70-41c4-8c57-122639d399cf)

![image](https://github.com/user-attachments/assets/bf1f58cc-7602-49b1-be59-eca0626d1366)

![image](https://github.com/user-attachments/assets/eade5b92-1d90-455c-8ba3-a4dfb3e2522e)

![image](https://github.com/user-attachments/assets/72a65504-1c94-4f44-98c9-7666f8f9311c)

![image](https://github.com/user-attachments/assets/094c499d-97c7-4a7d-90cb-bd5f1d75d9b8)

![image](https://github.com/user-attachments/assets/43b55831-c456-47b6-ab43-6810a654a0f4)

![image](https://github.com/user-attachments/assets/f0c889a4-2052-471a-a8e6-be2a6a806c83)

![image](https://github.com/user-attachments/assets/7f195185-4fdc-49dc-b47c-78be5200e003)

We use the abc -liberty command to find the convert the RTL to the netlist.

```bash
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```

After running the above code we get the below output

![image](https://github.com/user-attachments/assets/de274a9f-3028-4aa4-805b-7d1b98f835e7)

![image](https://github.com/user-attachments/assets/f8452fec-653e-432c-b27d-8782759e18f6)

The realised netlist is as follows:-

We run the following command:-

```bash
show
```

![image](https://github.com/user-attachments/assets/4ffd5218-e34a-46e6-aac0-733a4c98474e)


![image](https://github.com/user-attachments/assets/78e50e65-debc-46bb-a3d0-a0c7950f925b)

We observe a 2:1 mux block in our circuit.

Now we observe the netlist as shown below

```bash
write_verilog good_mux_netlist.v
```

![image](https://github.com/user-attachments/assets/abe85e16-dbb7-484c-9f9e-ab27f3873aab)

![image](https://github.com/user-attachments/assets/0ca641af-0735-4d02-adc9-dd91f3e8e231)

```bash
write_verilog -noattr good_mux_netlist.v
```

![image](https://github.com/user-attachments/assets/f0e2b102-014b-43f6-bd27-1aa6dd2a2e95)


![image](https://github.com/user-attachments/assets/e70c7f4d-e15b-4c2b-acec-dbaa3197eae7)


# Lab 4 ( Introduction to Lab 4)

The name of the library is sky130_fd_sc_hd__tt_025C_1v80.lib. Here sky130 is the name of the library where 130 is the technology node used. Here tt stands for typical. Libraries can be of different types including slow,fast and typical. The 025c is the temperature and v8 is the voltage. There are three parameters which determine the performance of the transistors namely :-
- Process
- Voltage
- Temperature

Process can be different for the same transistor and there can be imperfections in the device but we still want the device to function appropriately.
Similarly irrespective of voltage and temperature variations we need our device to work properly.

The .lib file is as follows. In this file we can observe the units of temperature. voltage, leakage power , current unit , resistance , capacitive load, etc.
![image](https://github.com/user-attachments/assets/2cf8ec72-3cbd-4fac-903a-ac1b906b3228)

We have already mentioned that the .lib file contains different cells and also different versions of the same cells as shown in the following figure.
![image](https://github.com/user-attachments/assets/314ca855-5528-4067-b2d3-e4b987fb818f)

We can also observe the power associated with different pins as shown in the below figure

![image](https://github.com/user-attachments/assets/cd013cac-7e59-4050-9e4b-0209af855a53)

Comparison of different gates:-

Here we have found the leakage power for all the different cases of the and gate.

and 2_0

![image](https://github.com/user-attachments/assets/abde8d8c-992e-4c3f-abb6-c1c05a604425)

and 2_2

![image](https://github.com/user-attachments/assets/eb257612-cabe-491d-8fac-284d810f372b)

and 2_4

![image](https://github.com/user-attachments/assets/612bb14a-bbb5-436e-b98d-a177cc5c72cd)

In this case the area is the largest and thus the power needed for getting the respective outputs is also the largest for this sizing.


# Lab 5 ( Hier Synthesis Flat Synthesis)

In this lab we will observe the synthesis of the file multiple_modules.v  . In this file we have invoked multiple modules and have interconnected the output of module 1 with that of the module 2 and have found the output.

![image](https://github.com/user-attachments/assets/8dca6c61-aef1-430d-b1af-5424aee2b425)

The following diagram shows us the number of different components used in implementing the above circuit.

![image](https://github.com/user-attachments/assets/75e31a31-655a-4fdb-bc25-b5f7cd254fdb)

![image](https://github.com/user-attachments/assets/45219c9a-6ee6-4279-9cfb-0fea6e6f3a93)

We get the following netlist:-

![image](https://github.com/user-attachments/assets/1a214d12-9b7b-4b38-bdb5-60d966b03ce4)

![image](https://github.com/user-attachments/assets/2672adb7-a27d-4437-84ee-553691e62d58)

![image](https://github.com/user-attachments/assets/74630c45-b97a-47e8-88f6-6ea4925960c5)

From the above code we can see that we are getting an or gate in the output.

We now move towards the flat synthesis. In the above code we can see that the hierarchy of the respective modules is preserved and we have seperate modules for the and and or gate but when we do the flatten synthesis we are instantiating all the gates inside one module. We can observe the difference as shown below.

![image](https://github.com/user-attachments/assets/0d9f0cf4-3dff-4b74-848b-1b0df69e15ee)

After doing the flat synthesis we get the following output:-

![image](https://github.com/user-attachments/assets/d1cf2ae4-a18f-415e-80ff-2e7c9dd0c209)

The difference between the earlier netlist and the flatten netlist is that in the previous case we could only see the blocks of u1 and u2 but here we can clearly observe the and and or gates in the netlist.

We will now synthesize only the sub module 1. We do this in circuits where there are multiple instances of the same module so that we can directly invoke the same netlist into different parts of the circuit rather than synthesizing the entire design at once. If we synthesize the entire design at once we may not get the optimized output but when we use the divide and conquer method in a large circuit we synthseize individual blocks respectively and stitch the design fabric in the end to get optimized results. This way we get a much more optimized circuit.

![image](https://github.com/user-attachments/assets/49ec3096-7f37-47ac-bf67-31fec38a213f)


![image](https://github.com/user-attachments/assets/4ee44440-60c3-429a-90df-ba12fa159aba)

We can observe that only 1 and gate is synthesized in this design

![image](https://github.com/user-attachments/assets/bc3594f2-b18b-4363-8c6f-815d84a2c28b)



![image](https://github.com/user-attachments/assets/96eb0154-7959-44cb-a993-23209e73ec46)


# Why Flops are important in a circuit

In a combinational circuit we implement a design but every gate in a circuit has its own propagation delay. Different gates have different delays in the circuit and due to these delays it is possible that momentarily we might get a different output than what is expected. This small change in actual output is what we call a glitch. As the size of the combinational circuit increases the glitches increase as the delays in the circuit will increase. Thus we put a flop at every stage in the circuit which feed the input into the combinational blocks only after being triggered by a clock in the design. Thus we eliminate the possibility of glitches in the output but it comes at a cost of large area due to addition of flops. We can also use the reset/set pins to set the initial values of the flops so that we do not feed in garbage values in the combinational circuit.



# Coding styles for flops

Note:- The below two codes are for aynchronous resets.

![image](https://github.com/user-attachments/assets/bf35cb17-4fc5-4980-b613-becede867861)

We can see that from the above code that the always block is triggered when either of the two conditions are met. If we see the positive edge aynchronous reset then we enter the block and change the output to 1'b0. In the other case we enter the block when we observe positive edge of the clock. When this condition is met the output of the clock is changed to the current input held by the flop. We are basically making a D Flip flop.



Note:- The following are for synchronous reset

![image](https://github.com/user-attachments/assets/6500242e-01cd-4bdc-8dba-f76b12aa60b2)

The difference in the above code and the previous codes is that in this case the reset is triggered only when the positive edge of the clock is triggered and is thus synchronous.


![image](https://github.com/user-attachments/assets/1a1fddb8-e4bb-4091-ba5a-0ad4464d793e)


Similarly for the above code the we can see two conditions. The only difference is that we have given both the synchronous and the asynchronous reset.

# LAB ( Synthesis Simulations)


![image](https://github.com/user-attachments/assets/112247ff-1cb8-4cbd-9e7a-cf657c181094)


## For Asynchronous reset

![image](https://github.com/user-attachments/assets/b10e224c-e39a-4d57-a40f-1f0a3f00cf87)

The output q corresponding to input d is observed immediately after the reset is changed without waiting for the next clock pulse

![image](https://github.com/user-attachments/assets/dafa20af-e5de-4e76-a9ef-19e8aca3bb27)

In the above figure we can observe that as soon as the asynchronous reset is triggered the output goes low without waiting for the clock edge.

## For Asynchronous set

![image](https://github.com/user-attachments/assets/a63e13ad-23a2-4b58-8513-e99b7b02c9c5)

The output q corresponding to input d is observed immediately after the set is changed without waiting for the next clock pulse

![image](https://github.com/user-attachments/assets/400a6cb7-ac7a-470b-873a-aa0910bc0479)


In the above figure we can observe that as soon as the asynchronous set is triggered the output goes high without waiting for the clock edge.

## For Synchronous reset

![image](https://github.com/user-attachments/assets/022e6312-a8b8-4a74-bc24-2abd3d16e1af)

We can see that the output q is observed only when the clock is triggered after the synchronous reset.

![image](https://github.com/user-attachments/assets/f3af7fdf-ab46-4743-b135-e64d0fbda606)

In the above figure we can observe that as soon as the asynchronous set is triggered the output goes high without waiting for the clock edge.


## Synthesis of Aysnchronous circuit

![image](https://github.com/user-attachments/assets/3f4f4c7b-e399-4c84-98d6-a56dfa9f7a8e)


![image](https://github.com/user-attachments/assets/ed1d5295-936e-4fd5-9e54-b4a64873c205)

![image](https://github.com/user-attachments/assets/6a971dc8-c10b-454d-9d96-f26bfea8573f)



We get the following circuit upon execution

![image](https://github.com/user-attachments/assets/4dd9d7eb-acd4-452d-a0f4-26c269d53d7b)

The library is having an active low reset so we are getting an inverter before the flop.



## Synthesis of Synchronous circuit

### For synchronous reset

![image](https://github.com/user-attachments/assets/b45b5df4-0c32-4ddc-8089-fa7815f55f95)


![image](https://github.com/user-attachments/assets/39ba5fa6-761a-4a85-a5a4-9105b35de87d)



![image](https://github.com/user-attachments/assets/1059a4d7-3745-425d-beec-8339c4f984c1)

![image](https://github.com/user-attachments/assets/116bb768-593f-426b-b026-e773fa0a8440)

Since we are having a synchronous active low reset we will have an inverter before the input.

![image](https://github.com/user-attachments/assets/10b265ad-25d6-4667-92a5-b045eac00078)


### For Synchronous set

![image](https://github.com/user-attachments/assets/5940e7f6-b721-415e-8091-eff1639dd1ce)

![image](https://github.com/user-attachments/assets/4623200a-4748-461b-941a-f0f7a66dd2f7)

![image](https://github.com/user-attachments/assets/a2f61b68-8a29-4dd6-b704-46e009d1b24c)

![image](https://github.com/user-attachments/assets/b58b8991-98cc-40f3-9bc9-a443e05dab62)


![image](https://github.com/user-attachments/assets/dcb403c9-2d6a-4345-b65b-670e71f3ba31)


In this case we do not have any set or reset pin


# Optimizations

### Multiplication with 2

![image](https://github.com/user-attachments/assets/cd427486-a097-4fca-b041-de208eea37d4)

We can observe that there is no mapping of standard cells.-


If we multiply a binary number with 2 the corresponsding number is just the original number appended with a 0 at the end. Thus we do not need to add any cell in the citcuit.

![image](https://github.com/user-attachments/assets/e402ff2d-1c80-46d5-84f0-b4097c060e4c)

![image](https://github.com/user-attachments/assets/2eb2e4b7-97fa-43bc-9e12-efd698ee180d)

We get the above netlist

### Multiplication with 8

![image](https://github.com/user-attachments/assets/6eb3cdb9-2928-468b-a4ae-b038b101ddf8)


![image](https://github.com/user-attachments/assets/5b208c45-d6d5-4ef3-89d9-7f5eb4cb74e1)


![image](https://github.com/user-attachments/assets/dd03f59c-c59b-49db-bdad-8a3f55be8023)


![image](https://github.com/user-attachments/assets/14ea6e31-37cb-4939-ba69-ccd789654a82)

If we multiply a number with 8 then we just have to concatenate the two numbers together and thus we do not require any standard cells in the circuit. Thus we get this optimized circuit.



# Combinational Logic Optimization

It is used to squeeze the logic to get the most optimized design. The most optimized design will be efficient in terms of area and power. The different techniques that are used are:-
- Constant Propagation


![image](https://github.com/user-attachments/assets/e861a35f-117d-4084-a092-cd7672094faa)

From the above figure we can see that if the value of A or B = 0 then effectively the design is an inverter which will reduce the number of transistors used in the design and thus we will get less power and area constraints.


- Boolean Logic Optimization


![image](https://github.com/user-attachments/assets/4bf32b98-6882-4566-9614-509a79c15913)

Here we can observe a chain of ternary operators. These conditions will be synthesized into a mux. We can thus evaluate the expression of output from these equations and thus reduce them further if possible in order to get an optimized solution.


# Sequential Logic Optimization

The techniques of sequential optimization are:-

- Sequential constant propagation :- We replace the entire flop circuit with a simple logic 1 or 0. This is only possible when certain conditions are met in the circuit and based on them we can infer the logic coming at the output under all cases and so we can reduce the entire block with logic 1 or 0.
- State Optimization:- Optimization of ununsed states.
- Cloning:- used for physical aware synthesis. This is useful during floorplaaning of the blocks. Based on the timing and physical constraints on the board the logic is optimiezed.
- Retiminig:- We redesign the circuit in such a way that the delays between different blocks of the circuit are adjusted such that we can operate at the maximum possible frequency.
- Sequential Logic Cloning:-

# LAB ( Combinational Logic Optimizations)

- We are trying to synthesize the following code. This is an and gate after simplication of the ternary operator. We run the following instructions in yosys to get the netlist as shown.

	![image](https://github.com/user-attachments/assets/b66f0643-9d32-405d-ae31-cf2e6262606c)
    
	![image](https://github.com/user-attachments/assets/23ebf842-25e2-4fe0-82ed-8b49daeee862)
    
	![image](https://github.com/user-attachments/assets/743a7f33-847c-46a3-bc52-d3e0ecb067f0)
    
	![image](https://github.com/user-attachments/assets/499bd057-65f1-46c4-a5da-500f3f7ffb19)
    
	We can see in the below image that only an and gate is synthesized as expected
    
	![image](https://github.com/user-attachments/assets/89fae131-aa3f-4ffa-a3b6-6a2e92449a99)
    
	The netlist is as follows:-
    
	![image](https://github.com/user-attachments/assets/f9476adb-a1d2-4087-9f7b-4469c3c673fa)



- We are now trying to synthesize the following code. This is an or gate.  We run the following instructions in yosys to get the netlist as shown.

  ![image](https://github.com/user-attachments/assets/fe726b64-7837-4a7d-9d5d-83727299b935)

  ![image](https://github.com/user-attachments/assets/1306307d-f134-42eb-98ab-d7cb348f2481)

  ![image](https://github.com/user-attachments/assets/689d1871-4aa4-4e2f-a625-a903b9cc068a)

  We can see that an or gate is synthesized.

  ![image](https://github.com/user-attachments/assets/cce1daf1-fa99-4058-b6d4-96ad9739920b)

  The netlist is as follows:-

  ![image](https://github.com/user-attachments/assets/3dd33ff7-c4aa-4373-bb5d-b25962787b86)


- We are now trying to synthesize the following code. This is 3 input and gate.  We run the following instructions in yosys to get the netlist as shown.
 
  ![image](https://github.com/user-attachments/assets/99e21361-c0d6-4d01-8e01-a05fc4f1bb24)

  ![image](https://github.com/user-attachments/assets/8363c2c9-eb24-4566-b96a-57321ef9e4f2)

  ![image](https://github.com/user-attachments/assets/2db4735f-9ba4-4fe9-a162-2ff90e935a61)

  ![image](https://github.com/user-attachments/assets/a289d88d-bde0-4687-a199-205aedac4734)




  The netlist is as follows:-

  ![image](https://github.com/user-attachments/assets/886cb576-99e0-40ce-a080-f6f7075ed646)


- We will now try to synthesize the following code for multiple modules opt

  ![image](https://github.com/user-attachments/assets/33467529-6bf1-4bb3-a298-17bc97530f22)


  ![image](https://github.com/user-attachments/assets/4beec00b-39dd-4db9-ba31-e9471ee582ae)

  ![image](https://github.com/user-attachments/assets/2183c22a-3cfa-4205-ad6c-58c76c04511d)

  ![image](https://github.com/user-attachments/assets/d42cbf80-8c11-4df5-a3bb-62de571d1fc8)

  ![image](https://github.com/user-attachments/assets/70662b39-1d54-451e-b2ab-0bfcd54f8e63)

  ![image](https://github.com/user-attachments/assets/4472db08-142b-438e-9575-6c067da49af6)

  The netlist is as follows:-

  ![image](https://github.com/user-attachments/assets/a183c9f4-f047-49aa-9a0f-731c406e91a9)

 
- We will now try to synthesize the following code for multiple modules opt2

  ![image](https://github.com/user-attachments/assets/f71f1c85-77e0-43d6-aba1-8825136bf501)

 
  ![image](https://github.com/user-attachments/assets/0108b803-fea9-45eb-b5f2-fa322f3b8eea)

  ![image](https://github.com/user-attachments/assets/2b7aa6c4-894a-44be-b3d1-412fead0e375)

  ![image](https://github.com/user-attachments/assets/b759aeda-c015-4b1f-a056-9aeb39850b0c)

  The netlist is as follows:-

  ![image](https://github.com/user-attachments/assets/654b3c08-fa19-4c8d-9b61-13ac87921ff3)

  # Sequential Logic Optimizations
  We are trying to optimize the d Flip flop using reset and set.

  The code is as follows:-

  ![image](https://github.com/user-attachments/assets/b3d17b78-8a81-4d1d-97ab-b5b0b8621c86)

 
  ## Simulated Output with reset
 
  ![image](https://github.com/user-attachments/assets/ed2d2093-6cd9-4064-920a-050ccdb626c5)

  In this case we can see that the output q is waiting for the edge of the clock to go to logic 1 after the change in reset.

  ![image](https://github.com/user-attachments/assets/737bf5e5-dbe0-4aae-ad69-bd13bb78cc42)

  We can see that a flop is inferred.


  The netlist is as follows:-

  ![image](https://github.com/user-attachments/assets/b5d9b3c6-0c21-4840-9377-af449f6d6a3b)


  ## Simulated Output with set

  ![image](https://github.com/user-attachments/assets/f0888439-80a8-414a-923e-d947c6a131e8)

  In this case we can observe that the output is throughout 1 and thus the entire circuit and can be replaced by a logic 1.

  ![image](https://github.com/user-attachments/assets/40e50463-aa6f-429d-904c-0f2957573ebd)

  No flop is inferred as shown above


  The netlist is as follows:-

  ![image](https://github.com/user-attachments/assets/d96937ed-dc46-42eb-b093-68fd8e5c5b6d)


  We can see that there is no requirement of any flop in this circuit so it is sequentially optimized.

  ## Simulated output with both reset and set

  Code:-

  ![image](https://github.com/user-attachments/assets/7a95be47-7496-4fc0-a223-be35e5aedc83)

  We can see that dffs are used in the layout:-

  ![image](https://github.com/user-attachments/assets/521d4a35-7828-4f78-b42f-039641af93ff)

  ![image](https://github.com/user-attachments/assets/100206eb-a451-4ac1-82d8-fc272684a7d4)



  The netlist is as follows:-


  ![image](https://github.com/user-attachments/assets/10fdf8c0-bacc-4738-995e-73cf870770b1)


  # Unused Output Optimization

  Code:-

  ![image](https://github.com/user-attachments/assets/95ddc228-8d9c-4428-b418-417e2e00c933)

  Here q is only sensing  the output q[0] and the rest bits are unused. So there is no need to map these 2 bits in the design. The bit q[0] toggles on every clock cycle. So we should get an inverter.

  After synthesis we can see that there is only 1 dff in the synthesized logic

  ![image](https://github.com/user-attachments/assets/0650828e-ec54-40cf-b5a2-c3eef8439d94)

  The netlist is as follows:-

 ![image](https://github.com/user-attachments/assets/f9482f2e-03db-4f14-907c-f0300513a275)


 Code:-

 ![image](https://github.com/user-attachments/assets/55b5bc9b-2491-473a-80b4-470cf7d78b96)


 In this case all the bits in the output are sensed and corresponding to that we are going to generate a netlist.

 ![image](https://github.com/user-attachments/assets/b7abf0e7-8939-4f70-a443-898a19e5edb3)

 We can see that 3 dff are synthesized


 The netlist is as follows:-

 ![image](https://github.com/user-attachments/assets/fd517ec8-e0e5-4aaa-b628-bd7ef344f44f)


 # Gate Level Simulation (GLS)

 Here we run the testbench for the netlist. Netlist is logically same as the code so we verify it using the same testbench which we used for the RTL code. We need to do this step to ensure the logical correctness of the code and to ensure the timing of the design is met.

 ![image](https://github.com/user-attachments/assets/ac2a341a-08c1-44f1-b211-7b71209d1363)

 Here if the gate level models are timing aware then we can use it for timing simulation. We need to validate the functionality as there are synthesis simulation mismatches.

 # Synthesis Simulation Mismatch

 - Missing Sensitivity List
   Simulator works based on activity. If there a change in the sensitivity then there is a change in output based on the conditions. If we miss some trigger conditions in the sensitivity list then the design will be wrong.
 - BLocking vs Non-Blocking Assignments ( evaluated inside always block)

   - Blocking statements ( = )
 	In this the statements are sequentially executed
   - Non Blocking Statements ( <= )
 	In this the statements are parallely executed
    
	 
 - Non standard coding

# Caveats with Blocking Statements

  Here if we interchange the order in which the statemnts are suppposed to be written inside the always block for a sequential circuit then the logic of the circuit can change.

  ![image](https://github.com/user-attachments/assets/1a3ce698-1fda-4f75-bc4b-199912f22c13)

  In the above code as we can see that we have used blocking statements inside the always block. Our aim is to have logic Y= (A+B)C. So we should or the logic a and b followed by and the resultant with c but since we have used the blocking statements and the order in which  we have written the code is wrong, incorrect logic will be synthesized.

# LAB ( Synthesis Simulation Mismatch)

Code:-

![image](https://github.com/user-attachments/assets/7c6cd8d5-0ecd-4d6f-aeb8-7b252668a13d)


Simulation Results:-

![image](https://github.com/user-attachments/assets/4cca88cc-e39e-4cf4-a01f-a1c53b174e01)

Synthesis:-

![image](https://github.com/user-attachments/assets/25f5898b-7f48-4991-8624-f04dbb095e4a)

![image](https://github.com/user-attachments/assets/e563fd2d-8d5f-4827-8f2f-a8bfd33bcf02)

![image](https://github.com/user-attachments/assets/0e5afe75-fb67-4f70-95b9-192de5fa10c0)


The netlist is as follows:-

![image](https://github.com/user-attachments/assets/0244799b-6f1b-4b37-986c-d625d904b659)


GLS simulation results

![image](https://github.com/user-attachments/assets/63f1a5d6-ec0f-4271-87b3-6ded1e7db741)

we observe the same results as seen earlier and it implies that there is no mismatch.


Code:-

![image](https://github.com/user-attachments/assets/2b768d5e-f86a-489b-87b5-72b1ca831a60)


Simulion Results:-

![image](https://github.com/user-attachments/assets/8584b899-b4e3-4e9e-ad12-4fa37cdac067)

Synthesis:-

![image](https://github.com/user-attachments/assets/c059fbb6-252c-469a-a59d-3997b660d51e)

![image](https://github.com/user-attachments/assets/c77ac7d6-b9d6-40b2-b698-80992e91c1c3)

![image](https://github.com/user-attachments/assets/72faf859-8a4f-44dd-ad89-671314ea68cf)



The netlist is as follows:-

![image](https://github.com/user-attachments/assets/a258cc50-f847-4c12-b954-e9e9869e1852)


GLS Simulation:-

![image](https://github.com/user-attachments/assets/e715d498-f693-48a4-b215-648d8c108e81)

Here we can observe a difference in the output after GLS Simulation. The output y follows i0 and i1 based on the input of the select line whereas during RTL simulation it follows the select line but does not reflect the changes in the values of i0 nad i1 at all times and acts like a flip flop.



## Mismatch Blocking Statement:-

Aim :- Our aim is to synthesize the logic Y = ( A + B ) . C

We want the or operation to take place followed by the and operation. Now we will simulate the code as given below.

Code:-

![image](https://github.com/user-attachments/assets/12bac8fe-4b58-4fe1-adaa-2d7aa4b4e7a1)


Simulation Results:-

![image](https://github.com/user-attachments/assets/20fddfcc-5727-430c-acca-bc8fd88963ef)

The output at the marked point should have been 1 but is 0. This is because of the mismatch due to the blocking statements where the code is run sequentially in the always block. The value of d is calculated first in the first statement which is followed by the calculation of x. In case we want to make this work we should reverse the order of statements written in the always block. Here the past value of x is taken for the current calculation and thus we are getting this output. Also x is synthesized as a flop.

Synthesis:-

![image](https://github.com/user-attachments/assets/31c76c9e-25b8-4053-8bd2-ab826ec9c2c9)

![image](https://github.com/user-attachments/assets/0abba558-381d-41cb-bc47-f0004583c915)

![image](https://github.com/user-attachments/assets/d07d4291-8945-4f0d-979b-3bf58a58a3ed)




The netlist is as follows:-

![image](https://github.com/user-attachments/assets/7c090c40-9be7-4f2e-bcb9-b3439156d6e6)

GLS Simulation:-

![image](https://github.com/user-attachments/assets/3e701ac6-6233-445b-88f6-7473f828823e)

If we observe the rtl simulation and compare it with the gls simulation results we can see that there is a mismatch between the outputs. This is due to the blocking statements used. The synthesized solution is looking at the present values of input and is calculating the output accordingly whereas in the rtl simulation the output is genrated based on the previous value of input.

# Conclusion:-

In the above course we have understood the conversion of the RTL Design to the gate level netlist using the library blocks. We have used the Yosys setup for this conversion. In order to verify the results in both the RTL and GLS simulation we have used the same testbench. We have studied the different types of libraries for the same gates or different gates which may be implemented based on the requirement of the end user based on the acceptable tradeoff. We have done the hier flatten synthesis where we have reduced the blocks in the netlist using the flatten command such that all the functionality of the multiple modules is executed within the top module thereby reducing the complexity of the design and the netlist. We have looked at different coding styles in RTL code and have found out which one is the best according to the code. We have also looked at codes like multiplication by 2 where the output can be directly inferred without the requirement of the different cells. We have also done the combinational and sequential logic optimizations alongwith the ununsed output optimizations. Lastly we have done the gate level synthesis where we have seen the synthesis simulation mismatch and the different reasons which lead to such mismatches.


</details>

<details>

 <summary> Assignment 10</summary>

 # Synthesize RISC-V and compare output with functional simulations 

 The RTL simulations done on the RISC V processor are as follows:-

 ![image](https://github.com/user-attachments/assets/2cbe1544-3d06-428d-912c-a02e150c54e2)

 The following was the digital and its corresponding analog output:- 

 ![image](https://github.com/user-attachments/assets/46512c2a-84ef-43e0-ac41-bd7401eff9bb)

 ![image](https://github.com/user-attachments/assets/bcace7d6-1fcf-409b-8b0a-0546653a1baa)




 We now need to synthesize the RTL and find out the corresponding output. We expect to get the standard cells in gtkwave alongwith the analog output. We will use yosys to synthesize the output.

 In order to synthesize the RTL we will use YOSYS.

 ```bash

 read_liberty <path>
 read_verilog <path>
 synth -top rvmyth
 abc -liberty <path>
 write_verilog rvmyth_net.v

```

![image](https://github.com/user-attachments/assets/babaf83e-d0a2-43ec-a9a8-31a57b0aff91)

![image](https://github.com/user-attachments/assets/0d82e1cf-819f-42d8-bee9-7967f37bc14c)

![image](https://github.com/user-attachments/assets/2695d233-ebc5-4d8e-b860-9779385fc169)




 We then need to add this rvmyth_net.v file to the testbench file.

 ![image](https://github.com/user-attachments/assets/60a84e9c-61d2-4948-bee9-879c923898bc)


 The netlist generated after the write_verilog command is as follows:-
 
 ![image](https://github.com/user-attachments/assets/ba832392-1565-408f-b16b-aa69701ad94a)

 ![image](https://github.com/user-attachments/assets/488ae646-251b-4233-9001-faf22c6bd271)



 After doing the synthesis we get the following output and we run the following files using iverilog to get the output on gtkwave.

 ![image](https://github.com/user-attachments/assets/d0fcec4b-4523-40b7-8b37-993a5a9bc4d8)

 The output observed on gtkwave is as follows:-

 ![image](https://github.com/user-attachments/assets/caa3d748-cd62-4b7d-ac05-a51f0dd5e878)

 The standard cells are as follows:-

 ![image](https://github.com/user-attachments/assets/8852c007-9068-4108-898e-adaeca3c2404)

 ![image](https://github.com/user-attachments/assets/a777d606-2bb3-4968-8808-d5ca6fe0e6ca)

 The output which we get after running the synthesized output is as follows:-

 ![image](https://github.com/user-attachments/assets/00d5d733-411b-4f4e-9023-4bdc8fdddd52)

 Conclusion:- From the above output we can observe a sawtooth waveform and thus we can say that the output O2 which we get from GLS is same as that of the functional simulation O1. Hence O1 = O2.







 

</details>












