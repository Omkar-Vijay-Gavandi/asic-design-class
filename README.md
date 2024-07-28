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

## Task 1:-
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
   
- ### Instruction Breakdown for the code given:
    - ### ADD r10, r11, r12
    
      - Type: R-Type
      - Opcode: 0110011
      - funct3: 000
      - funct7: 0000000
      - rs1: 11 (r11)
      - rs2: 12 (r12)
      - rd: 10 (r10)
      - <code style="color : name_color"> Binary encoding: 0000000 01100 01011 000 01010 0110011</code>
      
    - ### SUB r12, r10, r11

      - Type: R-Type
      - Opcode: 0110011
      - funct3: 000
      - funct7: 0100000
      - rs1: 10 (r10)
      - rs2: 11 (r11)
      - rd: 12 (r12)
      - <code style="color : name_color"> Binary encoding: 0100000 01011 01010 000 01100 0110011 </code>

    - ### AND r11, r10, r12
    
      - Type: R-Type
      - Opcode: 0110011
      - funct3: 111
      - funct7: 0000000
      - rs1: 10 (r10)
      - rs2: 12 (r12)
      - rd: 11 (r11)
      - <code style="color : name_color"> Binary encoding: 0000000 01100 01010 111 01011 0110011 </code>
 
    - ### OR r8, r11, r5
    
      - Type: R-Type
      - Opcode: 0110011
      - funct3: 110
      - funct7: 0000000
      - rs1: 11 (r11)
      - rs2: 5 (r5)
      - rd: 8 (r8)
      - <code style="color : name_color">Binary encoding: 0000000 00101 01011 110 01000 0110011 </code>

    - ### XOR r8, r10, r4
    
      - Type: R-Type
      - Opcode: 0110011
      - funct3: 100
      - funct7: 0000000
      - rs1: 10 (r10)
      - rs2: 4 (r4)
      - rd: 8 (r8) 
      - <code style="color : name_color"> Binary encoding: 0000000 00100 01010 100 01000 0110011 </code>

    - ### SLT r0, r1, r4
    
      - Type: R-Type
      - Opcode: 0110011
      - funct3: 010
      - funct7: 0000000
      - rs1: 1 (r1)
      - rs2: 4 (r4)
      - rd: 0 (r0)
      - <code style="color : name_color"> Binary encoding: 0000000 00100 00001 010 00000 0110011 </code>

    - ### ADDI r2, r2, 5
    
      - Type: I-Type
      - Opcode: 0010011
      - funct3: 000
      - imm[11:0]: 000000000101
      - rs1: 2 (r2)
      - rd: 2 (r2)
      - <code style="color : name_color"> Binary encoding: 000000000101 00010 000 00010 0010011 </code>
    
    - ### SW r2, r0, 4
    
      - Type: S-Type
      - Opcode: 0100011
      - funct3: 010
      - imm[11:5]: 0000000
      - rs1: 0 (r0)
      - rs2: 2 (r2)
      - imm[4:0]: 00100
      - <code style="color : name_color"> Binary encoding: 0000000 00010 00000 010 00100 0100011 </code>

    - ### SRL r6, r1, r1
    
      - Type: R-Type
      - Opcode: 0110011
      - funct3: 101
      - funct7: 0000000
      - rs1: 1 (r1)
      - rs2: 1 (r1)
      - rd: 6 (r6)
      - <code style="color : name_color"> Binary encoding: 0000000 00001 00001 101 00110 0110011 </code>

    - ### BNE r0, r0, 20
    
      - Type: B-Type
      - Opcode: 1100011
      - funct3: 001
      - imm[12]: 0
      - imm[10:5]: 000010
      - rs1: 0 (r0)
      - rs2: 0 (r0)
      - imm[4:1]: 0100
      - imm[11]: 0
      - <code style="color : name_color"> Binary encoding: 000000 00000 00000 001 0100 00000 1100011 </code>

    - ### BEQ r0, r0, 15
    
      - Type: B-Type
      - Opcode: 1100011
      - funct3: 000
      - imm[12]: 0
      - imm[10:5]: 000001
      - rs1: 0 (r0)
      - rs2: 0 (r0)
      - imm[4:1]: 1110
      - imm[11]: 0
      - <code style="color : name_color"> Binary encoding: 000000 00000 00000 000 1110 00000 1100011 </code>

    - ### LW r3, r1, 2
    
      - Type: I-Type
      - Opcode: 0000011
      - funct3: 010
      - imm[11:0]: 000000000010
      - rs1: 1 (r1)
      - rd: 3 (r3)
      - <code style="color : name_color"> Binary encoding: 000000000010 00001 010 00011 0000011 </code>

    - ### SLL r5, r1, r1
    
      - Type: R-Type
      - Opcode: 0110011
      - funct3: 001
      - funct7: 0000000
      - rs1: 1 (r1)
      - rs2: 1 (r1)
      - rd: 5 (r5)
      - <code style="color : name_color"> Binary encoding: 0000000 00001 00001 001 00101 0110011 </code>


## The final table for the instructions is as follows:-

| Assembly Instruction | Instruction format         |  Hexadecimal equivalent                             | Binary equivalent
|----------------------|----------------------------|-----------------------------------------------------|-------------------
| ADD r10, r11, r12    | R                          | <code style="color : name_color"> 0x00C58033 </code>| 0000 0000 1100 0101 1000 0101 0011 0011
| SUB r12, r10, r11    | R                          | <code style="color : name_color"> 0x40B50633 </code>| 0100 0000 1011 0101 0000 0110 0011 0011
| AND r11, r10, r12    | R                          | <code style="color : name_color"> 0x00C575B3 </code>| 0000 0000 1100 0101 0111 0101 1011 0011
| OR r8, r11, r5       | R                          | <code style="color : name_color"> 0x005B7833 </code>| 0000 0000 0101 0101 1110 0100 0011 0011
| XOR r8, r10, r4      | R                          | <code style="color : name_color"> 0x00454433 </code>| 0000 0000 0100 0101 0100 0100 0011 0011
| SLT r00, r1, r4      | R                          | <code style="color : name_color"> 0x0040A033 </code>| 0000 0000 0100 0000 1010 0000 0011 0011
| ADDI r02, r2, 5      | I                          | <code style="color : name_color"> 0x00510113 </code>| 0000 0000 0101 0001 0000 0001 0001 0011
| SW r2, r0, 4         | S                          | <code style="color : name_color"> 0x00204223 </code>| 0000 0000 0010 0000 0010 0001 0010 0011
| SRL r06, r01, r1     | R                          | <code style="color : name_color"> 0x0010D333 </code>| 0000 0000 0001 0000 1101 0011 0011 0011
| BNE r0, r0, 20       | B                          | <code style="color : name_color"> 0x00001463 </code>| 0000 0000 0000 0000 0001 0000 0110 0011
| BEQ r0, r0, 15       | B                          | <code style="color : name_color"> 0x00003863 </code>| 0000 0000 0000 0000 0000 0000 0110 0011
| LW r03, r01, 2       | I                          | <code style="color : name_color"> 0x0020A183 </code>| 0000 0000 0010 0000 1010 0001 1000 0011
| SLL r05, r01, r1     | R                          | <code style="color : name_color"> 0x001092B3 </code>| 0000 0000 0001 0000 1001 0010 1011 0011
 

### Task 2:-


