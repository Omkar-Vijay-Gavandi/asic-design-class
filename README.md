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

### The first instruction involves the stack pointer. Therefore in order to check the initial and final contents of the stack pointer we use the follwoing code. [O1]

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












