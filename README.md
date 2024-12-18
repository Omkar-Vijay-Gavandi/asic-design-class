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

<details>

 <summary> Assignment 11 </summary>

 # Static Timing analysis

 ### Checks

 ![image](https://github.com/user-attachments/assets/0f083030-12b0-4776-a1ee-36269dc77889)
 
 ![image](https://github.com/user-attachments/assets/025a8147-a586-45ea-98ef-e3c0e8f74942)

 ![image](https://github.com/user-attachments/assets/eac8d012-efee-41dd-8e19-35d2dc14c7e9)

 Here the yellow dots indicate the output ports/d pins


 ### Slack

 ![image](https://github.com/user-attachments/assets/31121173-5e5b-4bf7-b10f-6ec43c806a57)

 Difference between the arrival time and the required time.

 ![image](https://github.com/user-attachments/assets/e0a1c82c-725d-4843-8dd4-389c70055965)

 ![image](https://github.com/user-attachments/assets/905286d3-0fe1-466c-97bc-2c1447da70fd)

 ### Types of different checks

 ![image](https://github.com/user-attachments/assets/4a31c263-8506-485c-a9a0-1f40092620ce)

### Conversion of logic gates to nodes

![image](https://github.com/user-attachments/assets/74204488-4995-42db-a5af-ee5c901527bc)

### Actual arrival time calculation from the nodes

Arrival time:- It is the time when the signal is expected to arrive.

![image](https://github.com/user-attachments/assets/ffde5f4b-43b1-4144-a056-da568645fb92)

### Required Arrival time calculation from the nodes

It is the time when we expect the transition.

![image](https://github.com/user-attachments/assets/5dab4690-0dd3-4de8-acc5-f0dda2fce500)

This information is important when we there is a negative slack in the circuit and we need to find out which part of the circuit is contributing to the maximum negative slack so as to reduce it.

![image](https://github.com/user-attachments/assets/55fd4212-3d36-480b-9943-f1e9ca7bb483)

Assuming that the RAT is 7.55 at the output node we calculate RAT for each node as follows

### Slack calculation:-

![image](https://github.com/user-attachments/assets/428a10d7-ac24-4df4-8388-461049f42f5a)

We can do 2 types of analysis path based and graph based. From the above example we come to know that it is more realistic to do path based analysis as we analysing the circuit based on the path which will be followed by the input to the output for a particular input.

### Pin based analysis ( Pin to node conversion)

![image](https://github.com/user-attachments/assets/3b814acc-9d2a-497f-a863-6ab053258e71)

![image](https://github.com/user-attachments/assets/6ffed9de-888f-4e22-bcf4-63cef76f3b29)

### Setup Analysis:-

![image](https://github.com/user-attachments/assets/2b3fddd3-f85f-41f1-ad9c-a03e9a96b3b6)

## Transistor Level Circuits:-

### Negative and positive latch 

![image](https://github.com/user-attachments/assets/42f7413f-6f64-4cd8-a6f3-ebfac57aabbb)

![image](https://github.com/user-attachments/assets/ce57cb65-508c-4f1a-aacd-086ce61802cd)

### Eye diagram for jitter analysis

![image](https://github.com/user-attachments/assets/cce0ed89-7815-4de0-85e2-399412c4c520)

![image](https://github.com/user-attachments/assets/0f6fcd04-daa2-4db0-9497-86acfd5fba90)

Voltage and power supply variations lead to voltage droop and ground bounce as shown below

![image](https://github.com/user-attachments/assets/c20bd205-990b-4f2c-bec1-7c97eae9f6d9)

Final eye diagram

![image](https://github.com/user-attachments/assets/7266a591-b470-47d4-9434-0f31cbd71e08)

Jitter extraction in Setup timing analysis

![image](https://github.com/user-attachments/assets/50466b88-badb-41a4-af0e-ea70fc5c149b)

## Timing analysis:-

### Setup time

![image](https://github.com/user-attachments/assets/8c1c1bea-6410-4abb-8c11-61b5f088ac0f)

### Hold time

![image](https://github.com/user-attachments/assets/43b0e2af-bf54-45a2-ba88-984348f18f62)

## On Chip Variation

### Etching

![image](https://github.com/user-attachments/assets/661970f4-9be4-44aa-a2bb-899c8b57b8bc)

![image](https://github.com/user-attachments/assets/28a99393-d9e0-46e2-9e10-0fb51fb6afea)

The inverters in the center are adjustcent to other inverters so the variations in etching are less compared to those that are etched on the outskirts which might be connected to some flops or any other block.

### Relation between resistance , delay and drain current

![image](https://github.com/user-attachments/assets/1f875062-8f07-41a6-82a9-70ee97ed9856)

![image](https://github.com/user-attachments/assets/18be1724-216d-4eb3-9d59-99d4db1c3359)

### OCV setup time analysis

![image](https://github.com/user-attachments/assets/ed1055f2-6eef-43a1-ac0a-aa0d847e033f)

We vary the data arrival time or the data required time by 20% and find the corresponding slack

### Additional Pessimism

![image](https://github.com/user-attachments/assets/13eb1bb6-aa74-4c10-8b71-6f028121d588)

 Since the slack obatined in the previous case was negative we need to remove/add the pessimistic delay which we had considered in the common delay terms.


 ### OCV hold time analysis

 ![image](https://github.com/user-attachments/assets/f9ebb6d0-da0a-41f2-9d7b-f9441deb63ae)

 Since we are getting a negative slack in the above calculation we will have to add the additional pessimism value to the arrival time or remove it from the required time. After this we observe the slack as follows:-

 ![image](https://github.com/user-attachments/assets/c52db9ae-fd14-4426-91e3-b8f1976bf179)


 ### Clock Creation

 ![image](https://github.com/user-attachments/assets/ab00d450-dd74-408c-81de-2e62d7242226)


 # LAB

 We are using the OpenSTA tool for this Lab.

 We will use the following commands to do the task

 ```bash
read_liberty lib/sta/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog src/module/RV_CPU_netlist.v
link_design RV_CPU
```

The following commands are used to give the constraints according to the clock period given to me which is 9.5ns

```bash
create_clock -name clk -period 9.5 [get_ports clk]
set_clock_uncertainty [expr 0.05 * 9.5] -setup [get_clocks clk]
set_clock_uncertainty [expr 0.08 * 9.5] -hold [get_clocks clk]
set_clock_transition [expr 0.05 * 9.5] [get_clocks clk]
set_input_transition [expr 0.08 * 9.5] [all_inputs]
```
The below commands are used to generate the final report for the max and minimum path delay

```bash
report_checks -path_delay max
report_checks -path_delay min
```

The execution of the above code was done as below

![image](https://github.com/user-attachments/assets/334d1476-4b02-4af5-9c23-2dee989e80be)

The report for the maximum path delay:-

![image](https://github.com/user-attachments/assets/d644adfa-d6fb-4045-a877-47f2abebe5f9)

The report for the minimum path delay:-

![image](https://github.com/user-attachments/assets/21bda53b-baa9-448f-888d-ad33f5f32209)

### Conclusion:-

![image](https://github.com/user-attachments/assets/4a31c263-8506-485c-a9a0-1f40092620ce)


In the above diagram we can observe a launch and a capture flip flop. There are multiple ways to reach the output node based on the input which is given to the launch flip flop. Based on this input the arrival time and the required time is calculated in the node analysis as already explained before. Based on these values the slack was calculated at every node. The above is a reg2reg path report where we have calculated the maximum and the minimum path delay around the netlist that was generated in the previous lab.





 






































</details>




<details>

 <summary> Assignment 12 </summary>

 # PVT Corners in Semiconductor Devices

PVT corners refer to specific combinations of Process, Voltage, and Temperature (PVT) conditions that affect the performance of semiconductor devices, particularly in digital circuits. Understanding these corners is essential for ensuring that designs meet performance, power, and reliability specifications across different operating environments. Here’s a breakdown of each component:

## 1. Process (P)

- **Variation in Fabrication**: Different batches of chips may exhibit variations due to inconsistencies in the manufacturing process, such as doping levels, oxide thickness, or lithography variations.

### Types of Process Corners:
- **Fast**: Transistors are faster than nominal due to better-than-expected manufacturing conditions.
- **Slow**: Transistors are slower due to less favorable manufacturing conditions.

## 2. Voltage (V)

- **Supply Voltage Levels**: The operating voltage of the circuit can vary due to power supply fluctuations, droop, or variations in manufacturing.

### Types of Voltage Corners:
- **High Voltage (HV)**: The circuit operates at a voltage above the nominal level, which can lead to increased performance but may also cause higher power consumption.
- **Low Voltage (LV)**: The circuit operates at a voltage below the nominal level, which can reduce performance and increase the likelihood of timing violations.

## 3. Temperature (T)

- **Operating Environment**: Temperature affects the electrical characteristics of semiconductor materials, including mobility and threshold voltage.

### Types of Temperature Corners:
- **High Temperature (HT)**: Increased temperature can cause transistors to slow down and can affect leakage currents.
- **Low Temperature (LT)**: Lower temperatures can lead to improved performance but may also result in issues like increased threshold voltages.

## Common PVT Corners

Typically, PVT corners are analyzed in pairs, resulting in several combinations. The most common corners include:

### 1. Slow/Slow (SS):
- Slow process, low voltage, high temperature.
- Typically the worst-case scenario for timing analysis, as it can lead to the slowest circuit performance.

### 2. Fast/Fast (FF):
- Fast process, high voltage, low temperature.
- This represents the best-case scenario for timing analysis, where the circuit is expected to perform optimally.

### 3. Fast/Slow (FS):
- Fast process, low voltage, high temperature.
- This corner can present challenges as the circuit may perform better than expected but could still have timing issues due to low voltage and high temperature.

### 4. Slow/Fast (SF):
- Slow process, high voltage, low temperature.
- This corner can help identify cases where the circuit is under stress despite a higher supply voltage.

## Importance of PVT Corners
- **Timing Analysis**: PVT corners are critical for static timing analysis (STA) to ensure that the design meets timing requirements under worst-case conditions.
- **Design Robustness**: Understanding these corners helps designers create robust designs that function correctly across a range of operating conditions, ensuring reliability in real-world applications.
- **Power Consumption**: Different voltage and temperature conditions can impact power consumption, making it essential to analyze PVT corners during the design process.

By considering PVT corners in the design and verification phases, engineers can improve the overall performance and reliability of their circuits, minimizing risks associated with real-world variations in manufacturing and operating conditions.

# LAB

 The .sdc file is as follows:-
 
 ![image](https://github.com/user-attachments/assets/6b2f85f4-4e5a-4f03-9e1f-78d546bf3e41)

 The code for the same is as follows:-

 ``` bash
set_units -time ns
set PERIOD 9.5
create_clock [get_pins {pll/CLK}] -name clk -period $PERIOD
set_clock_uncertainty [expr 0.05 * $PERIOD] -setup [get_clocks clk]
set_clock_uncertainty [expr 0.08 * $PERIOD] -hold [get_clocks clk]
set_clock_transition [expr 0.05 * $PERIOD] [get_clocks clk]


set_input_transition [expr $PERIOD * 0.08] [get_ports ENB_CP]
set_input_transition [expr $PERIOD * 0.08] [get_ports ENB_VCO]
set_input_transition [expr $PERIOD * 0.08] [get_ports REF]
set_input_transition [expr $PERIOD * 0.08] [get_ports VCO_IN]
set_input_transition [expr $PERIOD * 0.08] [get_ports VREFH]

```

The tickle script is as follows:-

``` bash
set list_of_lib_files(1) "sky130_fd_sc_hd__ff_100C_1v65.lib"
set list_of_lib_files(2) "sky130_fd_sc_hd__ff_100C_1v95.lib"
set list_of_lib_files(3) "sky130_fd_sc_hd__ff_n40C_1v56.lib"
set list_of_lib_files(4) "sky130_fd_sc_hd__ff_n40C_1v65.lib"
set list_of_lib_files(5) "sky130_fd_sc_hd__ff_n40C_1v76.lib"
set list_of_lib_files(6) "sky130_fd_sc_hd__ff_n40C_1v95.lib"
set list_of_lib_files(7) "sky130_fd_sc_hd__ss_100C_1v40.lib"
set list_of_lib_files(8) "sky130_fd_sc_hd__ss_100C_1v60.lib"
set list_of_lib_files(9) "sky130_fd_sc_hd__ss_n40C_1v28.lib"
set list_of_lib_files(10) "sky130_fd_sc_hd__ss_n40C_1v35.lib"
set list_of_lib_files(11) "sky130_fd_sc_hd__ss_n40C_1v40.lib"
set list_of_lib_files(12) "sky130_fd_sc_hd__ss_n40C_1v44.lib"
set list_of_lib_files(13) "sky130_fd_sc_hd__ss_n40C_1v60.lib"
set list_of_lib_files(14) "sky130_fd_sc_hd__ss_n40C_1v76.lib"
set list_of_lib_files(15) "sky130_fd_sc_hd__tt_025C_1v80.lib"
set list_of_lib_files(16) "sky130_fd_sc_hd__tt_100C_1v80.lib"

for {set i 1} {$i <= [array size list_of_lib_files]} {incr i} {
read_liberty -min /home/omkarvijayagavandi/BabySoC_Simulation/src/$list_of_lib_files($i)
read_liberty -max /home/omkarvijayagavandi/BabySoC_Simulation/src/$list_of_lib_files($i)
read_liberty -min /home/omkarvijayagavandi/BabySoC_Simulation/src/avsdpll.lib
read_liberty -max /home/omkarvijayagavandi/BabySoC_Simulation/src/avsdpll.lib
read_liberty -min /home/omkarvijayagavandi/BabySoC_Simulation/src/avsddac.lib
read_liberty -max /home/omkarvijayagavandi/BabySoC_Simulation/src/avsddac.lib
read_verilog /home/omkarvijayagavandi/BabySoC_Simulation/src/vsdbabysoc_synth.v
link_design vsdbabysoc
current_design
read_sdc /home/omkarvijayagavandi/BabySoC_Simulation/src/vsdbabysoc_synthesis.sdc
check_setup -verbose
report_checks -path_delay min_max -fields {nets cap slew input_pins fanout} -digits {4} > /home/omkarvijayagavandi/BabySoC_Simulation/src/sta_output/min_max_$list_of_lib_files($i).txt

exec echo "$list_of_lib_files($i)" >> /home/omkarvijayagavandi/BabySoC_Simulation/src/sta_worst_max_slack.txt
report_worst_slack -max -digits {4} >> /home/omkarvijayagavandi/BabySoC_Simulation/src/sta_worst_max_slack.txt

exec echo "$list_of_lib_files($i)" >> /home/omkarvijayagavandi/BabySoC_Simulation/src/sta_worst_min_slack.txt
report_worst_slack -min -digits {4} >> /home/omkarvijayagavandi/BabySoC_Simulation/src/sta_worst_min_slack.txt

exec echo "$list_of_lib_files($i)" >> /home/omkarvijayagavandi/BabySoC_Simulation/src/sta_tns.txt
report_tns -digits {4} >> /home/omkarvijayagavandi/BabySoC_Simulation/src/sta_tns.txt

exec echo "$list_of_lib_files($i)" >> /home/omkarvijayagavandi/BabySoC_Simulation/src/sta_wns.txt
report_wns -digits {4} >> /home/omkarvijayagavandi/BabySoC_Simulation/src/sta_wns.txt
}
```

The above tickle script is executed using the following code:-

```bash
sta
source sta_pvt.tcl
```

The table for the sdc file is as follows:-

# Timing Analysis Table

This table summarizes the TNS (Total Negative Slack), WNS (Worst Negative Slack), and Worst Slack values for different libraries.

| Library                                 | TNS        | WNS        | Worst Setup Slack | Worst Hold Slack |
|-----------------------------------------|------------|------------|-------------------|-------------------|
| sky130_fd_sc_hd__ff_100C_1v65.lib      | 0          | 0          | 2.033             | -0.479            |
| sky130_fd_sc_hd__ff_100C_1v95.lib      | 0          | 0          | 3.5511            | -0.5373           |
| sky130_fd_sc_hd__ff_n40C_1v56.lib      | 0          | 0          | 0.2433            | -0.4192           |
| sky130_fd_sc_hd__ff_n40C_1v65.lib      | 0          | 0          | 1.3785            | -0.459            |
| sky130_fd_sc_hd__ff_n40C_1v76.lib      | 0          | 0          | 2.4022            | -0.4941           |
| sky130_fd_sc_hd__ff_n40C_1v95.lib      | 0          | 0          | 3.5712            | -0.5364           |
| sky130_fd_sc_hd__ss_100C_1v40.lib      | -3331.689  | -19.1841   | -19.1841          | 0.2487            |
| sky130_fd_sc_hd__ss_100C_1v60.lib      | -1365.2373 | -9.9309    | -9.9309           | -0.0274           |
| sky130_fd_sc_hd__ss_n40C_1v28.lib      | -15108.4385| -64.5234   | -64.5234          | 1.1491            |
| sky130_fd_sc_hd__ss_n40C_1v35.lib      | -9089.3223 | -41.7204   | -41.7204          | 0.6834            |
| sky130_fd_sc_hd__ss_n40C_1v40.lib      | -6469.6123 | -31.7278   | -31.7278          | 0.4606            |
| sky130_fd_sc_hd__ss_n40C_1v44.lib      | -5002.271  | -25.9241   | -25.9241          | 0.3234            |
| sky130_fd_sc_hd__ss_n40C_1v60.lib      | -1882.5096 | -12.6494   | -12.6494          | -0.0061           |
| sky130_fd_sc_hd__ss_n40C_1v76.lib      | -729.3387  | -6.3564    | -6.3564           | -0.2197           |
| sky130_fd_sc_hd__tt_025C_1v80.lib      | -2.4261    | -0.0875    | -0.0875           | -0.4167           |
| sky130_fd_sc_hd__tt_100C_1v80.lib      | 0          | 0          | 0.0678            | -0.4184           |

The timing analysis is as follows:-

The graph for the Total negative slack for all the above mentioned lib files is as follows:-

![image](https://github.com/user-attachments/assets/2a7d94da-f084-48eb-887b-2bfa39e1d411)

The graph for the Worst negative slack for all the above mentioned lib files is as follows:-

![image](https://github.com/user-attachments/assets/9e449b86-1faa-4f8c-a139-1caf9fd05f0e)

The graph for the Worst Setup slack for all the above mentioned lib files is as follows:-

![image](https://github.com/user-attachments/assets/0b7c32f0-9895-4ab0-b031-cfe819dd79fd)

The graph for the Worst Hold slack for all the above mentioned lib files is as follows:-

![image](https://github.com/user-attachments/assets/ec8ce2d2-62d3-4fe4-a589-0c56cb2f8ff6)



</details>


<details>	
	<summary> Assignment 13  </summary>
	
# Advanced Physical Design Using OpenLane/Sky130 Workshop

## Overview

### Package
In embedded boards, the "chip" we see is actually the **package**, which serves as a protective layer for the actual manufactured chip located at its center. Connections from the package to the chip are made via **wire bonding**, a basic wired connection method.

<p align="center">
  <img src="https://github.com/user-attachments/assets/190b4c19-7a10-4526-a449-c61955ef81e9" width="400" />
  <img src="https://github.com/user-attachments/assets/140d21ef-072e-44ba-9412-fe6485b6e3cf" width="400" />
  <img src="https://github.com/user-attachments/assets/8f941ff2-8377-44df-9c29-829f2d656ccd" width="400" />
</p>

### Chip
Inside the chip, signals from external sources are routed through **pads**. The area bound by these pads is the **core**, where all digital logic resides. Together, the core and pads form the **die**, which is the primary manufacturing unit in semiconductor production.

<p align="center">
  <img src="https://github.com/user-attachments/assets/07531d75-0042-4124-8e5d-e6a1315bdfa1" width="500" />
</p>

### Foundry
A **foundry** manufactures semiconductor chips, and **Foundry IPs** are intellectual properties specific to each foundry, often requiring high-level expertise. Reusable logic blocks are known as **macros**.

<p align="center">
  <img src="https://github.com/user-attachments/assets/b9fd0168-4a71-4e9a-9152-f7bd8a3f9cb6" width="500" />
</p>

## Instruction Set Architecture (ISA)

For a program written in C to run on hardware, a specific flow is followed:
1. The C program is first compiled into **assembly language** (e.g., **RISC-V ISA**).
2. This assembly code is converted into **machine language**, which is then read by the computer hardware.
3. The machine language is implemented using an **RTL** (Hardware Description Language).
4. Finally, the design progresses through a standard **RTL to GDSII flow**.

<p align="center">
  <img src="https://github.com/user-attachments/assets/f9f9c0ce-b464-4efc-92f2-3b40a0bff34a" width="500" />
</p>

### System Software Layers
For applications to run on hardware, **system software layers** (such as OS, compiler, and assembler) convert high-level code into binary language.

<p align="center">
  <img src="https://github.com/user-attachments/assets/e7d4317a-5dcc-48bf-b20d-d48465951c12" width="500" />
</p>

### Example Flow: Stopwatch App on RISC-V Core
For instance, in a stopwatch app:
- The OS layer might output a C function, which the compiler then converts into RISC-V instructions.
- The assembler then translates these instructions into machine language, which the chip layout understands.

<p align="center">
  <img src="https://github.com/user-attachments/assets/f56f5088-e623-4030-be95-0dd48c28f275" width="400" />
  <img src="https://github.com/user-attachments/assets/b3b41fed-fb8c-43eb-af67-3f845f0e1f2d" width="400" />
</p>

### RTL to Physical Design

After the assembler generates machine language, RTL (in HDL) implements specific instructions, synthesizing them into a **netlist** of gates for chip fabrication.

<p align="center">
  <img src="https://github.com/user-attachments/assets/b330eb3e-1e89-4da3-bcaa-e95fe6b118e3" width="500" />
</p>

---

## Open-Source Implementation of ASIC Design

**Open-source ASIC Design** requires:
- **RTL Designs**
- **EDA Tools**
- **PDK Data**

#### Evolution of ASIC Design
In 1979, **Lynn Conway** and **Carver Mead** proposed decoupling IC design from fabrication, leading to the concept of **Fabless Companies**. This shift allowed designers and pure-play fabs to work independently, interfacing through **Process Design Kits (PDKs)**, which contain data models, technology information, and design rules.

**Open-source PDK**: Google and Skywater opened up the Skywater 130nm PDK in June 2020, marking a milestone in public accessibility for ASIC design.

<p align="center">
  <img src="https://github.com/user-attachments/assets/e9fa7771-ef5d-4755-9f3f-18856e722039" width="500" />
</p>

## OpenLane: An Open-source ASIC Design Flow

The **OpenLane ASIC Design Flow** aims to transform the design from **RTL** (Register Transfer Level) to **GDSII**, the final layout format for fabrication.

<p align="center">
  <img src="https://github.com/user-attachments/assets/288edd23-d1e7-49a7-9dc6-7a93fc019575" width="500" />
</p>

### Key Stages in ASIC Flow

#### Synthesis
The RTL is synthesized into a circuit using **Standard Cell Libraries (SCL)**, resulting in a **Gate-Level Netlist** that is functionally equivalent to the RTL.

<p align="center">
  <img src="https://github.com/user-attachments/assets/6102211f-3af2-491a-a368-3919bb8e45a2" width="500" />
</p>

#### Standard Cell Libraries
Standard cells, as fundamental building blocks, have regular layouts and various views (e.g., GDSII, Liberty, SPICE/CDL).

<p align="center">
  <img src="https://github.com/user-attachments/assets/1fcaa7bf-b7c6-4fc4-a7cd-5747a6045682" width="500" />
</p>

#### Floor Planning
Defines the chip's overall structure and includes **core and I/O placement**.

<p align="center">
  <img src="https://github.com/user-attachments/assets/ddb33f57-72b5-4dac-a9bf-fde5782b6bae" width="400" />
  <img src="https://github.com/user-attachments/assets/ab93e598-e4b4-4b61-adee-80f51fb9c4c4" width="400" />
</p>

#### Power Planning
Typically uses upper metal layers for **power distribution** due to their lower resistance, helping to minimize **IR drops**.

<p align="center">
  <img src="https://github.com/user-attachments/assets/be885ab5-06ca-47f9-ac4c-f2625b63453e" width="500" />
</p>

#### Placement
- **Global Placement**: Provides approximate cell locations based on connectivity.
- **Detailed Placement**: Adjusts positions to ensure legal, non-overlapping cell locations.

<p align="center">
  <img src="https://github.com/user-attachments/assets/4e0c6519-c1a8-4be3-bfe5-9c2b8a70e139" width="500" />
  <img src="https://github.com/user-attachments/assets/01915ce1-6694-4eee-8df3-2b37039b7809" width="500" />
</p>

#### Clock Tree Synthesis
Addresses **clock skew** to ensure synchronous operation across all components.

<p align="center">
  <img src="https://github.com/user-attachments/assets/060cf6a0-1ef9-4a31-abc2-799487dd8d06" width="500" />
</p>

#### Routing
OpenLane uses **6 routing layers** in Skywater PDK, with the lowest being Titanium Nitride and the remaining five being aluminum.

<p align="center">
  <img src="https://github.com/user-attachments/assets/2c6125b9-91ff-4aa0-8fa6-c52605fa0ca1" width="500" />
  <img src="https://github.com/user-attachments/assets/459f1066-49d8-41b6-97a0-c133c943fb8d" width="500" />
</p>

### Final Layout & Sign-Off Checks

Once routing is complete, the layout undergoes multiple checks:
- **DRC (Design Rule Checking)** ensures layout adherence to fabrication rules.
- **LVS (Layout vs. Schematic)** verifies the final layout's functionality against the original netlist.
- **STA (Static Timing Analysis)** confirms the design meets its timing requirements.

<p align="center">
  <img src="https://github.com/user-attachments/assets/8ab63b14-c047-488f-adb9-e401c4ce72cc" width="500" />
</p>


# Synthesizing the 'picorv32a' Design in OpenLANE

This guide details the synthesis process for the `picorv32a` design in OpenLANE, focusing on calculating the **Flip-Flop (Flop) Ratio** and presenting key synthesis metrics.

## Task 1: Synthesis

1. **Run Synthesis for `picorv32a`:**  
   - Start by synthesizing the `picorv32a` design using the **OpenLANE ASIC design flow**. This process converts the RTL description into a gate-level netlist based on the chosen standard cell library.
   - After synthesis, review the outputs, which will include the generated **netlist** and key **synthesis reports**.

   <div align="center">
      <img src="https://github.com/user-attachments/assets/000f1b00-9e21-49a9-8d6d-850df8ba77af" alt="Synthesis Output" />
   </div>

## Task 2: Calculating the Flip-Flop (Flop) Ratio

The **Flop Ratio** provides a measure of the balance between sequential and combinational logic in the design, impacting **area, power, and timing characteristics**.

- **Formula for Flop Ratio:**

   \[
   \text{Flop Ratio} = \frac{\text{Number of D Flip-Flops}}{\text{Total Cell Count}}
   \]

   - **Percentage of Flop Ratio:**

   \[
   \text{Percentage of Flop Ratio} = \text{Flop Ratio} \times 100
   \]

### Synthesis Results for `picorv32a`

- **Number of D Flip-Flops:** 1634
- **Total Cell Count:** 14846
- **Flop Ratio:** 0.11
- **Percentage Flop Ratio:** 11.01%

   <div align="center">
      <img src="https://github.com/user-attachments/assets/d945921f-7f11-4106-b0e5-2de6c738f32f" alt="Flip Flop Ratio Calculation" />
   </div>

   <div align="center">
      <img src="https://github.com/user-attachments/assets/72faa55d-d832-49f8-b142-c7d05152bc75" alt="Flop Ratio Result" />
   </div>

   <div align="center">
      <img src="https://github.com/user-attachments/assets/b7ec39e4-8aff-4ea9-b4b9-685050fbddb0" alt="Percentage Flop Ratio Result" />
   </div>


**Day2:**

## Good Floorpan vs Bad Floorplan and Introduction to Library Cell:


### Utilisation factor and aspect ratio

![image](https://github.com/user-attachments/assets/f84c8015-f922-43ed-822c-28f4904cbd75)

Define the area of the netlist

![image](https://github.com/user-attachments/assets/d1cf3165-75c2-4d79-b8aa-9936344b6396)

The above picture demonstrates the calculation of the utilisation factor

### Cooncept of pre-placed cells

![image](https://github.com/user-attachments/assets/86be9e67-98e5-41bb-94f1-4a492541f526)

We need to define the placement of some of the cells in the circuit. Some of them are mentioned above. These cells are defined only once but they can be invoked into the design multiple times. The arrangement of these cells needs to be done in the floorplanning part.

![image](https://github.com/user-attachments/assets/de6b4796-5edc-466a-8ad7-9801588aee48)

The above are the pre-placed cells and once placed they cannot be removed.

### De-Coupling Capacitors

![image](https://github.com/user-attachments/assets/27708263-eac3-413e-b096-d72f7b897c04)

From the above figure we can see that there is a lot of distance between the source and the blocks where the design is implemented. The wire between VDD and the blocks also has some resistnace and thus there is a drop in voltage from VDD to a value less than VDD. If this value is less than the value of the noise margin then the output voltage may not be detected thus leading to the introduction of crosstalk.

![image](https://github.com/user-attachments/assets/ae4c3372-97ab-4a1f-8353-42d87d9cebd0)

So in order to solve this above problem we introduce a decoupling capacitor in the design which will feed the supply to the logic during every transition.

![image](https://github.com/user-attachments/assets/4e1764bd-c766-49e4-80e7-ad6777125452)

The placed cells look like the below diagram

![image](https://github.com/user-attachments/assets/c1096618-360e-4be2-b956-d60a262a1cdd)

### Power Planning

![image](https://github.com/user-attachments/assets/b1a3315c-2451-4027-88b6-0506093d221e)

In order for the driver to maintain the required voltage levels we need to make sure that the power supply is supplying the voltage VDD regularly.

![image](https://github.com/user-attachments/assets/05dd703b-dd5e-4fa8-b0b8-6c7ffcf768fd)

For the above 16 bit bus we can see that there is a ground bounce as all the logic 1 will try to discharge to 0 at the same time. Similar things are obseved in the other case wherein we observe a voltage droop.

![image](https://github.com/user-attachments/assets/ad469a4a-5024-4343-a6ae-17c36c43b32d)

In order to solve this problem we introduce seperate supply and ground lines in the circuit.

![image](https://github.com/user-attachments/assets/090cc517-3287-43d3-88f8-744e860b6065)

The floopplanning looks like this

### Pin placement and logical cell placement blockage

![image](https://github.com/user-attachments/assets/7dde7b11-bcfb-4efa-ad63-347f8809bc4d)

From the above block we can understand that the reason behind the arrangement of the pins in the respective positions, i.e to decrease the amount of delay or power ,etc. We also add the logical cell placement blockage so that no other pins are mapped in the package.












-----
Tasks:

1. Run 'picorv32a' design floorplan using OpenLANE flow and generate necessary outputs.
2. Calculate the die area in microns from the values in floorplan def.
3. Load generated floorplan def in magic tool and explore the floorplan.
4. Run 'picorv32a' design congestion aware placement using OpenLANE flow and generate necessary outputs.
5. Load generated placement def in magic tool and explore the placement.
	 Area of Die in microns = Die width in microns ∗ Die height in microns

-----
# Change directory to the OpenLANE working directory
cd ~/Desktop/work/tools/openlane_working_dir/openlane

# (Optional) If the OpenLANE flow Docker container is not aliased, you can run this command to start the container
# alias docker='docker run -it -v $(pwd):/openLANE_flow -v $PDK_ROOT:$PDK_ROOT -e PDK_ROOT=$PDK_ROOT -u $(id -u $USER):$(id -g $USER) efabless/openlane:v0.21'

# Enter the OpenLANE Docker container to run the OpenLANE flow interactively
docker

# Once inside the OpenLANE flow Docker container, run the following to start OpenLANE in interactive mode
./flow.tcl -interactive

# Load the OpenLANE package (this is required for the flow to work properly)
package require openlane 0.9

# Prepare the 'picorv32a' design by creating the necessary files and directories
prep -design picorv32a

# After preparation, run the synthesis process to convert RTL to a gate-level netlist
run_synthesis

# Now, initiate the floorplanning process
run_floorplan


![image](https://github.com/user-attachments/assets/9bd50e64-145a-46c6-9d97-a9ef1aec1a26)

![image](https://github.com/user-attachments/assets/78d2b5b5-ade6-499f-adf3-ac700e4d436c)

![image](https://github.com/user-attachments/assets/be99a56d-313e-43f4-b23c-bea525040fb5)


According to floorplan def
	1000   Unit Distance  = 1 micron
	Die width in unit distance = 660685 − 0 = 660685
	Die height in unit distance = 671405 − 0 = 671405
	Distance in microns = Value in unit distance / 1000
	Die width in microns = 660685/1000 = 660.685 microns
	Die height in microns = 671405/1000 = 671.405 microns
	Are os die in microns = 660.685 ∗ 671.405 = 443587.212425 square microns

![image](https://github.com/user-attachments/assets/5e5dfb55-0542-405f-98a4-31d37d491cc5)

3. Load generated floorplan def in magic tool and explore the floorplan.

   Commands to load floorplan def in magic in another terminal

bash
# Change directory to path containing generated floorplan def
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/17-03_12-06/results/floorplan/

# Command to load the floorplan def in magic tool
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &


The magic window opens as follows:-

![image](https://github.com/user-attachments/assets/2a6acfd3-bfd9-4fcc-8acc-e75a49985f64)

## Library Binding and Placement

![image](https://github.com/user-attachments/assets/8b84780b-1f13-4d62-9aca-748d98709c44)

The above netlist is represeneted in the form of blocks as shown below

![image](https://github.com/user-attachments/assets/b3787bc9-0ac9-4133-884d-a7d8924247f0)

The same cells can have different areas due to which the delays increase/decrease and thus we have different flavours of the same cells


![image](https://github.com/user-attachments/assets/30c243f0-2f85-4224-a533-274c17458aa7)

### Optimize placement using estimated wire-length and capacitance

![image](https://github.com/user-attachments/assets/5c308552-6c09-49f1-a82f-f6382f96ac38)


We can see that there is a lot of distance between some of the blocks because of which there can be some problems associated with delays,noise margin. In order to solve them we need to optimize the circuit. We add repeaters in the cirucit.


![image](https://github.com/user-attachments/assets/32e8dbce-eeb8-4600-ab7e-f818649b5527)


As we can see in the above case we are adding a buffer between Din2 and its corresponding logic in order to get the respective logic in the cicuit.

The final floorplanned view looks like this


![image](https://github.com/user-attachments/assets/81d7896a-b56b-46a8-9257-61c83135f839)

### Need for libraries and characterization


![image](https://github.com/user-attachments/assets/7fd96476-84d8-40a8-a540-8a73e44d57d9)

In the above diagram we can the multiple stages involved in the implementation of a logic in the circuit. 


![image](https://github.com/user-attachments/assets/10eaf417-dd48-4232-966a-a2bb660d45f0)

### Congestion aware placement using Replace

We run placement and get the following results using the commands specified

bash
# Change directory to path containing generated placement def
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/17-03_12-06/results/placement/

# Command to load the placement def in magic tool
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &


![image](https://github.com/user-attachments/assets/47e48b06-5044-4119-bf48-76f8bedc08c0)

![image](https://github.com/user-attachments/assets/79c1ab35-a5f0-4d88-890f-21d0456da8c2)


## Cell design and characterization flows

The cell design flow involves all the below mentioned checks.

![image](https://github.com/user-attachments/assets/73828dd2-43fb-4b97-9ef3-ea9f0a8475ae)

## General timing characterization parameters

### Timing threshold definitions

The following timing characterisations are to be considered:-

![image](https://github.com/user-attachments/assets/0a3be2dc-ca1c-43ab-8f65-056ec9c9d46c)


![image](https://github.com/user-attachments/assets/ca3186a8-2091-47e9-be60-102901ecb3d2)


![image](https://github.com/user-attachments/assets/a6b3301c-6e23-4861-bb2f-f1fe089dc6a3)

### Propagation delay and transition time

The threshold points should be specified correctly so as to not get a negative propagation delay as follows:-


![image](https://github.com/user-attachments/assets/3d00c499-7a00-4ddd-b52c-beb05049e5f5)

If the input slew is very high then we may also get a negative propagation delay


![image](https://github.com/user-attachments/assets/3c3ca1dd-8dc5-436d-8a20-1b56e436568a)

Considering all the above problems we have now defined the timing thresholds as follows:-


![image](https://github.com/user-attachments/assets/95820043-8a21-47f4-8528-c5720a3efa98)


# Day 3 - Design library cell using Magic Layout and ngspice characterization

### Theory

### Implementation

* Section 3 tasks:-
1. Clone custom inverter standard cell design from github repository: [Standard cell design and characterization using OpenLANE flow](https://github.com/nickson-jose/vsdstdcelldesign).
2. Load the custom inverter layout in magic and explore.
3. Spice extraction of inverter in magic.
4. Editing the spice model file for analysis through simulation.
5. Post-layout ngspice simulations.
6. Find problem in the DRC section of the old magic tech file for the skywater process and fix them.

#### 1. Clone custom inverter standard cell design from github repository

```bash
# Change directory to openlane
cd Desktop/work/tools/openlane_working_dir/openlane

# Clone the repository with custom inverter design
git clone https://github.com/nickson-jose/vsdstdcelldesign

# Change into repository directory
cd vsdstdcelldesign

# Copy magic tech file to the repo directory for easy access
cp /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech .

# Check contents whether everything is present
ls

# Command to open custom inverter layout in magic
magic -T sky130A.tech sky130_inv.mag &
```

Screenshot of commands run

![image](https://github.com/user-attachments/assets/5919b771-6225-4706-a6ec-94f339f71f13)

#### 2. Load the custom inverter layout in magic and explore.

Screenshot of custom inverter layout in magic

![image](https://github.com/user-attachments/assets/2f8fe008-6187-4490-b6d7-b1b56ad0e678)

Identifying NMOS and PMOS

![image](https://github.com/user-attachments/assets/2341ce05-5718-4217-9c05-5fc10a58c2ad)

![image](https://github.com/user-attachments/assets/814a0998-b039-43ff-969f-35b6304ff3d4)

Output Y attached in the inverter

![image](https://github.com/user-attachments/assets/50de1af8-f6c8-4029-8afb-978b44ad1a01)

PMOS cell

![image](https://github.com/user-attachments/assets/fcdf0c87-e9ad-4704-820e-77fb3856f098)

NMOS cell

![image](https://github.com/user-attachments/assets/7287e748-a415-4f74-a01b-9592873aa9b1)

#### 3. Spice extraction of inverter in magic.

Commands for spice extraction of the custom inverter layout to be used in tkcon window of magic

```tcl
# Check current directory
pwd

# Extraction command to extract to .ext format
extract all

# Before converting ext to spice this command enable the parasitic extraction also
ext2spice cthresh 0 rthresh 0

# Converting to ext to spice
ext2spice
```

Screenshot of tkcon window after running above commands

![image](https://github.com/user-attachments/assets/c488053c-95b2-443f-91a6-090d03766440)

![image](https://github.com/user-attachments/assets/fe61fe8a-8bad-4cd4-952c-152ecec1f5b6)

#### 4. Editing the spice model file for analysis through simulation.

Measuring unit distance in layout grid

![image](https://github.com/user-attachments/assets/0682d3e3-f44e-4b82-9db8-dd69de193545)

Final edited spice file ready for ngspice simulation

![image](https://github.com/user-attachments/assets/a00b1a14-2106-4f21-9e2c-e8d0f3201775)

#### 5. Post-layout ngspice simulations.

Commands for ngspice simulation

```bash
# Command to directly load spice file for simulation to ngspice
ngspice omk_inv.spice

# Now that we have entered ngspice with the simulation spice file loaded we just have to load the plot
plot y vs time a
```
Screenshots of ngspice run

![image](https://github.com/user-attachments/assets/2b7be60b-e908-4312-a625-e99dfaf21481)

Plots:-

![image](https://github.com/user-attachments/assets/0567ecae-789d-4481-82bb-0042d49b7c64)



## Rise Transition Time Calculation

math
Rise transition time = Time taken for output to rise to 80% - Time taken for output to rise to 20%

math
20% of output = 660 mV

math
80% of output = 2.64 V


20% Screenshots

![image](https://github.com/user-attachments/assets/6b5675ee-c9d0-4420-bb29-bb89c7e2bedc)

![image](https://github.com/user-attachments/assets/1f8be12e-6fca-44a5-a89f-a04094dccdc9)


80% Screenshots

![image](https://github.com/user-attachments/assets/b7468d08-57e8-48e0-be81-f4827a9b687e)

![image](https://github.com/user-attachments/assets/5b12cd30-45fe-475c-a908-4a9aa6a5608c)

math
Rise transition time = 2.23624 - 2.19211 = 0.06396 ns = 44.13 ps


## Fall transition time calculation

math
Fall transition time = Time taken for output to fall to 20% - Time taken for output to fall to 80%

math
20% of output = 660 mV

math
80% of output = 2.64 V


20% Screenshots

![image](https://github.com/user-attachments/assets/2a3378c4-3739-4928-bef0-ac2e94bd51b0)

![image](https://github.com/user-attachments/assets/95e3d290-cd91-4d13-9d86-ec7de28fd89b)



80% Screenshots

![image](https://github.com/user-attachments/assets/5548200e-e0a5-4f64-9627-4d0caf4da432)

![image](https://github.com/user-attachments/assets/6cf3ca0d-1f46-4619-9dd4-40d2a4964acd)


math
Fall transition time = 4.09526 - 4.01962 = 0.07564 ns = 75.64 ps


## Rise Cell Delay Calculation

math
Rise Cell Delay = Time taken for output to rise to 50% - Time taken for input to fall to 50%

math
50% of 3.3 V = 1.65 V


50% Screenshots

![image](https://github.com/user-attachments/assets/bee7742e-82a0-46d1-ad8d-1a034c0aef1c)



math
Rise Cell Delay = 2.13378 - 2.1274 = 0.06136 ns = 6.38 ps


## Fall Cell Delay Calculation

math
Fall Cell Delay = Time taken for output to fall to 50% - Time taken for input to rise to 50%

math
50% of 3.3 V = 1.65 V

50% Screenshots

![image](https://github.com/user-attachments/assets/465f7dc0-7248-4cf8-9472-c0323bc029ba)

![image](https://github.com/user-attachments/assets/9fb8783e-ca4f-4985-b527-a7d05b4dbc96)



math
Fall Cell Delay = 4.0779 - 4.05017 = 0.02 ns = 27.73 p

#### 6. Find problem in the DRC section of the old magic tech file for the skywater process and fix them.

Link to Sky130 Periphery rules: [https://skywater-pdk.readthedocs.io/en/main/rules/periphery.html](https://skywater-pdk.readthedocs.io/en/main/rules/periphery.html)

Commands to download and view the corrupted skywater process magic tech file and associated files to perform drc corrections

```bash
# Change to home directory
cd

# Command to download the lab files
wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz

# Since lab file is compressed command to extract it
tar xfz drc_tests.tgz

# Change directory into the lab folder
cd drc_tests

# List all files and directories present in the current directory
ls -al

# Command to view .magicrc file
gvim .magicrc

# Command to open magic tool in better graphics
magic -d XR &
```

Screenshots of commands run

![image](https://github.com/user-attachments/assets/05e1fb9c-bd59-49b2-8a17-0e60cf8e0f87)
![image](https://github.com/user-attachments/assets/59ae0d71-4a7d-40f4-a358-7e7b609fcdd6)


Screenshot of .magicrc file

![image](https://github.com/user-attachments/assets/3e69a8c3-71b7-4756-b1c7-d5e4481a6334)

**Incorrectly implemented poly.9 simple rule correction**

Screenshot of poly rules

![Screenshot from 2024-03-21 22-54-49](https://github.com/fayizferosh/soc-design-and-planning-nasscom-vsd/assets/63997454/9260cf37-5933-44a1-8362-597183644334)

Incorrectly implemented poly.9 rule no drc violation even though spacing < 0.48u

![image](https://github.com/user-attachments/assets/67cf6acf-1650-428f-860d-f90b66ada79d)

![image](https://github.com/user-attachments/assets/ba0ac3cf-c9f3-4af9-b43d-e52cd6bc7c7c)

New commands inserted in sky130A.tech file to update drc

![image](https://github.com/user-attachments/assets/d0eaee4f-6783-4b51-a89a-5367bcedab5f)

Commands to run in tkcon window

```tcl
# Loading updated tech file
tech load sky130A.tech

# Must re-run drc check to see updated drc errors
drc check

# Selecting region displaying the new errors and getting the error messages 
drc why
```

Screenshot of magic window with rule implemented

![image](https://github.com/user-attachments/assets/d62c2bcd-0f9f-407a-9fde-b565f718ddb2)
![image](https://github.com/user-attachments/assets/1aef0897-1e68-4cf1-89cc-380206719ea2)


Incorrectly implemented difftap.2 rule no drc violation even though spacing < 0.42u

![Screenshot from 2024-03-22 00-14-36](https://github.com/fayizferosh/soc-design-and-planning-nasscom-vsd/assets/63997454/a2d0d739-2df5-4eb5-ab78-c80d366e24e4)

New commands inserted in sky130A.tech file to update drc

![image](https://github.com/user-attachments/assets/12a4c099-5915-46ad-926d-cfe293fe9b80)

Commands to run in tkcon window

```tcl
# Loading updated tech file
tech load sky130A.tech

# Must re-run drc check to see updated drc errors
drc check

# Selecting region displaying the new errors and getting the error messages 
drc why
```

Screenshot of magic window with rule implemented

![image](https://github.com/user-attachments/assets/efa7d012-73cc-40ef-938e-bba7bf9db758)


**Incorrectly implemented nwell.4 complex rule correction**

Screenshot of nwell rules

![Screenshot from 2024-03-22 00-51-34](https://github.com/fayizferosh/soc-design-and-planning-nasscom-vsd/assets/63997454/4ad4901d-0b9a-4339-89e3-7bb3fce2766d)

Incorrectly implemented nwell.4 rule no drc violation even though no tap present in nwell

![image](https://github.com/user-attachments/assets/cd3eaaea-a443-4821-8db0-26a25ae139b7)

New commands inserted in sky130A.tech file to update drc

![image](https://github.com/user-attachments/assets/1467039b-3d91-4094-b962-165f93025ae8)
![image](https://github.com/user-attachments/assets/61515107-4a54-432c-80e1-ff06a5b6d015)

Commands to run in tkcon window

```tcl
# Loading updated tech file
tech load sky130A.tech

# Change drc style to drc full
drc style drc(full)

# Must re-run drc check to see updated drc errors
drc check

# Selecting region displaying the new errors and getting the error messages 
drc why
```
Screenshot of magic window with rule implemented

![image](https://github.com/user-attachments/assets/54bf9b5c-bf53-40ad-9d0e-64a109295b7f)


## Day 4

### Theory

### Implementation

* Section 4 tasks:-
1. Fix up small DRC errors and verify the design is ready to be inserted into our flow.
2. Save the finalized layout with custom name and open it.
3. Generate lef from the layout.
4. Copy the newly generated lef and associated required lib files to 'picorv32a' design 'src' directory.
5. Edit 'config.tcl' to change lib file and add the new extra lef into the openlane flow.
6. Run openlane flow synthesis with newly inserted custom inverter cell.
7. Remove/reduce the newly introduced violations with the introduction of custom inverter cell by modifying design parameters.
8. Once synthesis has accepted our custom inverter we can now run floorplan and placement and verify the cell is accepted in PnR flow.
9. Do Post-Synthesis timing analysis with OpenSTA tool.
10. Make timing ECO fixes to remove all violations.
11. Replace the old netlist with the new netlist generated after timing ECO fix and implement the floorplan, placement and cts.
12. Post-CTS OpenROAD timing analysis.
13. Explore post-CTS OpenROAD timing analysis by removing 'sky130_fd_sc_hd__clkbuf_1' cell from clock buffer list variable 'CTS_CLK_BUFFER_LIST'.

* Section 4 - Tasks 1 to 4 files, reports and logs can be found in the following folder:

[Section 4 - Tasks 1 to 4 \(vsdstdcelldesign\)](https://github.com/fayizferosh/soc-design-and-planning-nasscom-vsd/tree/main/Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign)

* Section 4 - Task 4 files, reports and logs can be found in the following folder:

[Section 4 - Task 4 \(src\)](https://github.com/fayizferosh/soc-design-and-planning-nasscom-vsd/tree/main/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src)

* Section 4 - Task 5 files, reports and logs can be found in the following folder:

[Section 4 - Task 5 \(picorv32a\)](https://github.com/fayizferosh/soc-design-and-planning-nasscom-vsd/tree/main/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a)

* Section 4 - Tasks 6 to 8 & 11 to 13 logs, reports and results can be found in following run folder:

[Section 4 - Tasks 6 to 8 & 11 to 13 Run \(24-03_10-03\)](https://github.com/fayizferosh/soc-design-and-planning-nasscom-vsd/tree/main/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/24-03_10-03)

* Section 4 - Tasks 9 to 11 logs, reports and results can be found in following run folder:

[Section 4 - Tasks 9 to 11 Run \(25-03_18-52\)](https://github.com/fayizferosh/soc-design-and-planning-nasscom-vsd/tree/main/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/25-03_18-52)

#### 1. Fix up small DRC errors and verify the design is ready to be inserted into our flow.

Conditions to be verified before moving forward with custom designed cell layout:
* Condition 1: The input and output ports of the standard cell should lie on the intersection of the vertical and horizontal tracks.
* Condition 2: Width of the standard cell should be odd multiples of the horizontal track pitch.
* Condition 3: Height of the standard cell should be even multiples of the vertical track pitch.

Commands to open the custom inverter layout

```bash
# Change directory to vsdstdcelldesign
cd Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign

# Command to open custom inverter layout in magic
magic -T sky130A.tech sky130_inv.mag &
```

Screenshot of tracks.info of sky130_fd_sc_hd

![image](https://github.com/user-attachments/assets/609eb728-f536-490b-92a4-db0a57bec6b2)

Commands for tkcon window to set grid as tracks of locali layer

```tcl
# Get syntax for grid command
help grid

# Set grid values accordingly
grid 0.46um 0.34um 0.23um 0.17um
```

![image](https://github.com/user-attachments/assets/b18c3357-f4f6-4fa1-a2b1-a824d471c2c7)

Condition 1 verified

![image](https://github.com/user-attachments/assets/4c979fe0-4a8d-476a-805a-5afe93106f68)

Condition 2 verified

```math
Horizontal\ track\ pitch = 0.46\ um
```

![image](https://github.com/user-attachments/assets/dd696de0-52c8-4181-bf75-3c23bd13af9d)

```math
Width\ of\ standard\ cell = 1.38\ um = 0.46 * 3
```

Condition 3 verified

```math
Vertical\ track\ pitch = 0.42\ um
```

![image](https://github.com/user-attachments/assets/a30a6096-3cc2-4707-8c83-ae8326c30bec)

```math
Height\ of\ standard\ cell = 2.72\ um = 0.34 * 8
```

#### 2. Save the finalized layout with custom name and open it.

Command for tkcon window to save the layout with custom name

```tcl
# Command to save as
save omk_inv.mag
```

Command to open the newly saved layout

```bash
# Command to open custom inverter layout in magic
magic -T sky130A.tech omk_inv.mag &
```

Screenshot of newly saved layout

![image](https://github.com/user-attachments/assets/2870c7be-aafe-47e9-88e4-1a73640819cd)

#### 3. Generate lef from the layout.

Command for tkcon window to write lef

```tcl
# lef command
lef write
```

Screenshot of command run

![image](https://github.com/user-attachments/assets/eb0ee006-1a98-4ae3-a95f-2fdb608208be)


Screenshot of newly created lef file

![image](https://github.com/user-attachments/assets/4dcb1aaf-d225-48bc-ad6a-5d12a305a56d)

#### 4. Copy the newly generated lef and associated required lib files to 'picorv32a' design 'src' directory.

Commands to copy necessary files to 'picorv32a' design 'src' directory

```bash
# Copy lef file
cp omk_inv.lef ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/

# List and check whether it's copied
ls ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/

# Copy lib files
cp libs/sky130_fd_sc_hd__* ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/

# List and check whether it's copied
ls ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/
```

Screenshot of commands run

![image](https://github.com/user-attachments/assets/a0121aac-187e-4c18-bcf9-2c756c5e3dcd)

#### 5. Edit 'config.tcl' to change lib file and add the new extra lef into the openlane flow.

Commands to be added to config.tcl to include our custom cell in the openlane flow

```tcl
set ::env(LIB_SYNTH) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"
set ::env(LIB_FASTEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__fast.lib"
set ::env(LIB_SLOWEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__slow.lib"
set ::env(LIB_TYPICAL) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"

set ::env(EXTRA_LEFS) [glob $::env(OPENLANE_ROOT)/designs/$::env(DESIGN_NAME)/src/*.lef]
```

Edited config.tcl to include the added lef and change library to ones we added in src directory

![image](https://github.com/user-attachments/assets/619d9764-b45f-40f9-b698-a484f471ab44)

#### 6. Run openlane flow synthesis with newly inserted custom inverter cell.

Commands to invoke the OpenLANE flow include new lef and perform synthesis 

```bash
# Change directory to openlane flow directory
cd Desktop/work/tools/openlane_working_dir/openlane

# alias docker='docker run -it -v $(pwd):/openLANE_flow -v $PDK_ROOT:$PDK_ROOT -e PDK_ROOT=$PDK_ROOT -u $(id -u $USER):$(id -g $USER) efabless/openlane:v0.21'
# Since we have aliased the long command to 'docker' we can invoke the OpenLANE flow docker sub-system by just running this command
docker
```
```tcl
# Now that we have entered the OpenLANE flow contained docker sub-system we can invoke the OpenLANE flow in the Interactive mode using the following command
./flow.tcl -interactive

# Now that OpenLANE flow is open we have to input the required packages for proper functionality of the OpenLANE flow
package require openlane 0.9

# Now the OpenLANE flow is ready to run any design and initially we have to prep the design creating some necessary files and directories for running a specific design which in our case is 'picorv32a'
prep -design picorv32a

# Adiitional commands to include newly added lef to openlane flow
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis
```

Screenshots of commands run

![image](https://github.com/user-attachments/assets/e0b6b98f-7cb4-4fb5-89e5-a43cea2748e8)

![image](https://github.com/user-attachments/assets/ed47a9d7-bc40-454e-a529-7ec2820ae011)

#### 7. Remove/reduce the newly introduced violations with the introduction of custom inverter cell by modifying design parameters.

Noting down current design values generated before modifying parameters to improve timing

![image](https://github.com/user-attachments/assets/2d97c619-f371-4c3a-9bca-577e72a10796)
![image](https://github.com/user-attachments/assets/8a47fdbd-e240-4518-93bb-b704594c5420)

Commands to view and change parameters to improve timing and run synthesis

```tcl
# Now once again we have to prep design so as to update variables
prep -design picorv32a -tag 14-11_05-21 -overwrite

# Addiitional commands to include newly added lef to openlane flow merged.lef
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

# Command to display current value of variable SYNTH_STRATEGY
echo $::env(SYNTH_STRATEGY)

# Command to set new value for SYNTH_STRATEGY
set ::env(SYNTH_STRATEGY) "DELAY 3"

# Command to display current value of variable SYNTH_BUFFERING to check whether it's enabled
echo $::env(SYNTH_BUFFERING)

# Command to display current value of variable SYNTH_SIZING
echo $::env(SYNTH_SIZING)

# Command to set new value for SYNTH_SIZING
set ::env(SYNTH_SIZING) 1

# Command to display current value of variable SYNTH_DRIVING_CELL to check whether it's the proper cell or not
echo $::env(SYNTH_DRIVING_CELL)

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis
```

Screenshot of merged.lef in `tmp` directory with our custom inverter as macro

![image](https://github.com/user-attachments/assets/ae716c92-8d68-453c-bc41-266197f01d77)

Screenshots of commands run

![image](https://github.com/user-attachments/assets/728e4441-bbbf-4feb-818f-303976a579f4)

![image](https://github.com/user-attachments/assets/94bcf300-1efc-481a-a51d-4c0fd3bc3b73)

Comparing to previously noted run values area has increased and worst negative slack has become 0

![image](https://github.com/user-attachments/assets/d7b9f3c5-fa38-47ff-8cc6-4c97a2aed9f8)

![image](https://github.com/user-attachments/assets/0dbdc420-29dd-4a06-afc6-31065227395e)

#### 8. Once synthesis has accepted our custom inverter we can now run floorplan and placement and verify the cell is accepted in PnR flow.

Now that our custom inverter is properly accepted in synthesis we can now run floorplan using following command

```tcl
# Now we can run floorplan
run_floorplan
```

Screenshots of command run

![image](https://github.com/user-attachments/assets/3f8dbff0-b92a-492f-9178-2c8100e43fed)

![image](https://github.com/user-attachments/assets/6d0630ae-be46-4382-8d71-d8144074abc0)

Since we are facing unexpected un-explainable error while using `run_floorplan` command, we can instead use the following set of commands available based on information from `Desktop/work/tools/openlane_working_dir/openlane/scripts/tcl_commands/floorplan.tcl` and also based on `Floorplan Commands` section in `Desktop/work/tools/openlane_working_dir/openlane/docs/source/OpenLANE_commands.md`

```tcl
# Follwing commands are alltogather sourced in "run_floorplan" command
init_floorplan
place_io
tap_decap_or
```

Screenshots of commands run

![image](https://github.com/user-attachments/assets/d73010dd-18f6-4934-ade0-1ac475d30cb0)

![image](https://github.com/user-attachments/assets/b65c0692-d698-47d7-99df-85b3a4a497c6)

![image](https://github.com/user-attachments/assets/97962b1f-285f-4c1f-ad98-c370a7e73970)

Now that floorplan is done we can do placement using following command

```tcl
# Now we are ready to run placement
run_placement
```
Screenshots of command run

![image](https://github.com/user-attachments/assets/92bde400-42a0-4b25-ba50-fdebb74dbb7c)

![image](https://github.com/user-attachments/assets/f994435d-5a26-4874-a163-85fd6b912ea9)

Commands to load placement def in magic in another terminal

```bash
# Change directory to path containing generated placement def
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/24-03_10-03/results/placement/

# Command to load the placement def in magic tool
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &
```
Screenshot of command

![image](https://github.com/user-attachments/assets/d4a9adf0-cc8b-4ecb-8cf4-c643c34bbff8)

Screenshot of placement def in magic

![image](https://github.com/user-attachments/assets/22f6e9a6-7547-4fce-8d34-9eb28fca0d55)

Screenshot of custom inverter inserted in placement def with proper abutment

![image](https://github.com/user-attachments/assets/f4037dd3-5dfb-4b6f-8904-5aac6cd1d94c)

Command for tkcon window to view internal layers of cells

```tcl
# Command to view internal connectivity layers
expand
```

Abutment of power pins with other cell from library clearly visible

![image](https://github.com/user-attachments/assets/594048b2-bc8c-48ba-ac0d-59ca4d64437e)

![image](https://github.com/user-attachments/assets/74470218-71a2-4f46-b182-c0e2afbc1c98)

![image](https://github.com/user-attachments/assets/7e6e9c6f-c2d1-4165-933e-ac58c75b81b5)

![image](https://github.com/user-attachments/assets/e5642c2c-f941-4110-b6d8-a156f3a9e14d)

#### 9. Do Post-Synthesis timing analysis with OpenSTA tool.

Since we are having 0 wns after improved timing run we are going to do timing analysis on initial run of synthesis which has lots of violations and no parameters were added to improve timing

Commands to invoke the OpenLANE flow include new lef and perform synthesis 

```bash
# Change directory to openlane flow directory
cd Desktop/work/tools/openlane_working_dir/openlane

# alias docker='docker run -it -v $(pwd):/openLANE_flow -v $PDK_ROOT:$PDK_ROOT -e PDK_ROOT=$PDK_ROOT -u $(id -u $USER):$(id -g $USER) efabless/openlane:v0.21'
# Since we have aliased the long command to 'docker' we can invoke the OpenLANE flow docker sub-system by just running this command
docker
```
```tcl
# Now that we have entered the OpenLANE flow contained docker sub-system we can invoke the OpenLANE flow in the Interactive mode using the following command
./flow.tcl -interactive

# Now that OpenLANE flow is open we have to input the required packages for proper functionality of the OpenLANE flow
package require openlane 0.9

# Now the OpenLANE flow is ready to run any design and initially we have to prep the design creating some necessary files and directories for running a specific design which in our case is 'picorv32a'
prep -design picorv32a

# Adiitional commands to include newly added lef to openlane flow
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

# Command to set new value for SYNTH_SIZING
set ::env(SYNTH_SIZING) 1

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis
```

Commands run final screenshot

![image](https://github.com/user-attachments/assets/0ab77308-e2d5-4b2d-af2e-37f5e1f7bb7c)

![image](https://github.com/user-attachments/assets/3cabbe4d-a463-4fff-9ddc-53e0a11ca8d4)

Newly created `pre_sta.conf` for STA analysis in `openlane` directory

![image](https://github.com/user-attachments/assets/f8d0c6dc-d147-4451-a44d-b38f292ac29f)

Newly created `my_base.sdc` for STA analysis in `openlane/designs/picorv32a/src` directory based on the file `openlane/scripts/base.sdc`

![image](https://github.com/user-attachments/assets/0cc50e27-28c9-4523-ad2b-9b019addbe83)

Commands to run STA in another terminal

```bash
# Change directory to openlane
cd Desktop/work/tools/openlane_working_dir/openlane

# Command to invoke OpenSTA tool with script
sta pre_sta.conf
```

Screenshots of commands run

![image](https://github.com/user-attachments/assets/cd492fbb-6c11-4f99-ba29-453e46c54d60)

![image](https://github.com/user-attachments/assets/49a15d09-7d87-4fa1-a313-7e8b76ba155d)

![image](https://github.com/user-attachments/assets/fe7133a9-8f62-4fa9-8d0b-99ecaa878f20)

![image](https://github.com/user-attachments/assets/07a81f1a-8b2a-4ab5-bc20-01274d052b22)

soc-design-and-planning-nasscom-vsd/assets/63997454/ab396c91-430f-41ca-b9a4-dda72a91c4d5)
![Screenshot from 2024-03-26 06-08-51](https://github.com/fayizferosh/soc-design-and-planning-nasscom-vsd/assets/63997454/aa1d50b0-9cb1-45bf-a641-b64842166b48)

Since more fanout is causing more delay we can add parameter to reduce fanout and do synthesis again

Commands to include new lef and perform synthesis 

```tcl
# Now the OpenLANE flow is ready to run any design and initially we have to prep the design creating some necessary files and directories for running a specific design which in our case is 'picorv32a'
prep -design picorv32a -tag 25-03_18-52 -overwrite

# Adiitional commands to include newly added lef to openlane flow
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

# Command to set new value for SYNTH_SIZING
set ::env(SYNTH_SIZING) 1

# Command to set new value for SYNTH_MAX_FANOUT
set ::env(SYNTH_MAX_FANOUT) 4

# Command to display current value of variable SYNTH_DRIVING_CELL to check whether it's the proper cell or not
echo $::env(SYNTH_DRIVING_CELL)

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis
```

Commands run final screenshot

![image](https://github.com/user-attachments/assets/013c2f82-17ec-4175-8a87-a80e4afbdd25)

![image](https://github.com/user-attachments/assets/b85638e5-4102-4d7e-9cfa-b18c0d20fc5b)

Commands to run STA in another terminal

```bash
# Change directory to openlane
cd Desktop/work/tools/openlane_working_dir/openlane

# Command to invoke OpenSTA tool with script
sta pre_sta.conf
```

Screenshots of commands run

![image](https://github.com/user-attachments/assets/8c5d471d-7701-42db-8bfb-24a773eef14a)

#### 10. Make timing ECO fixes to remove all violations.

OR gate of drive strength 2 is driving 4 fanouts

![image](https://github.com/user-attachments/assets/95926700-ad58-4240-b229-c6b9cbe8a03e)

Commands to perform analysis and optimize timing by replacing with OR gate of drive strength 4

```tcl
# Reports all the connections to a net
report_net -connections _11672_

# Checking command syntax
help replace_cell

# Replacing cell
replace_cell _14510_ sky130_fd_sc_hd__or3_4

# Generating custom timing report
report_checks -fields {net cap slew input_pins} -digits 4
```

Result - slack reduced

![image](https://github.com/user-attachments/assets/943eef87-69a4-4f60-b7fe-e757b439b334)

![image](https://github.com/user-attachments/assets/bc6fdae6-ae16-465c-b504-9719daeee7c7)

![image](https://github.com/user-attachments/assets/77963267-e264-455c-9a1e-4576e222f83c)

OR gate of drive strength 2 driving OA gate has more delay

![image](https://github.com/user-attachments/assets/ee48c029-29e2-49ce-be76-b4a9bc7df5dd)

Commands to perform analysis and optimize timing by replacing with OR gate of drive strength 4

```tcl
# Reports all the connections to a net
report_net -connections _11668_

# Replacing cell
replace_cell _14506_ sky130_fd_sc_hd__or4_4

# Generating custom timing report
report_checks -fields {net cap slew input_pins} -digits 4
```

Result - slack reduced

![image](https://github.com/user-attachments/assets/809e504c-1374-4fb0-8a06-76bdd1bb3ad4)

![image](https://github.com/user-attachments/assets/a24fdcd7-7acb-436d-93e0-41971bfad22d)

Commands to verify instance `_14506_`  is replaced with `sky130_fd_sc_hd__or4_4`

```tcl
# Generating custom timing report
report_checks -from _29043_ -to _30440_ -through _14506_
```

Screenshot of replaced instance

![image](https://github.com/user-attachments/assets/3c0d7dc5-cd3b-4999-8463-c88bf0908eed)

*We started ECO fixes at wns -23.5092 and now we stand at wns -23.1405 we reduced around 0.3687ns of violation*

#### 11. Replace the old netlist with the new netlist generated after timing ECO fix and implement the floorplan, placement and cts.

Now to insert this updated netlist to PnR flow and we can use `write_verilog` and overwrite the synthesis netlist but before that we are going to make a copy of the old old netlist

Commands to make copy of netlist

```bash
# Change from home directory to synthesis results directory
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/25-03_18-52/results/synthesis/

# List contents of the directory
ls

# Copy and rename the netlist
cp picorv32a.synthesis.v picorv32a.synthesis_old.v

# List contents of the directory
ls
```

Screenshot of commands run

![image](https://github.com/user-attachments/assets/aa0f1af2-b1d8-4d0d-bc82-2b841f635ed2)

Commands to write verilog

```tcl
# Check syntax
help write_verilog

# Overwriting current synthesis netlist
write_verilog /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/25-03_18-52/results/synthesis/picorv32a.synthesis.v

# Exit from OpenSTA since timing analysis is done
exit
```

Screenshot of commands run

![image](https://github.com/user-attachments/assets/d887267b-0c0d-4d0c-b8b9-bc026888e57e)

![image](https://github.com/user-attachments/assets/7db770b7-21a4-4cc8-947e-ffad12feccb8)

Since we confirmed that netlist is replaced and will be loaded in PnR but since we want to follow up on the earlier 0 violation design we are continuing with the clean design to further stages

Commands load the design and run necessary stages

```tcl
# Now once again we have to prep design so as to update variables
prep -design picorv32a -tag 24-03_10-03 -overwrite

# Addiitional commands to include newly added lef to openlane flow merged.lef
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

# Command to set new value for SYNTH_STRATEGY
set ::env(SYNTH_STRATEGY) "DELAY 3"

# Command to set new value for SYNTH_SIZING
set ::env(SYNTH_SIZING) 1

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis

# Follwing commands are alltogather sourced in "run_floorplan" command
init_floorplan
place_io
tap_decap_or

# Now we are ready to run placement
run_placement

# Incase getting error
unset ::env(LIB_CTS)

# With placement done we are now ready to run CTS
run_cts
```

Screenshots of commands run

![image](https://github.com/user-attachments/assets/2baa0415-31b5-487a-a869-5c8664d31aa6)

![image](https://github.com/user-attachments/assets/11d81a5d-ae9f-47b1-9407-44663fc84aa2)

![image](https://github.com/user-attachments/assets/e304ea9b-07bb-4237-920c-6baa6f608598)

![image](https://github.com/user-attachments/assets/69614496-aeba-4fe3-ba2c-9d2db065056d)

![image](https://github.com/user-attachments/assets/584a3d39-ca38-4b11-a257-68f3f26fc0c9)

#### 12. Post-CTS OpenROAD timing analysis.

Commands to be run in OpenLANE flow to do OpenROAD timing analysis with integrated OpenSTA in OpenROAD

```tcl
# Command to run OpenROAD tool
openroad

# Reading lef file
read_lef /openLANE_flow/designs/picorv32a/runs/24-03_10-03/tmp/merged.lef

# Reading def file
read_def /openLANE_flow/designs/picorv32a/runs/24-03_10-03/results/cts/picorv32a.cts.def

# Creating an OpenROAD database to work with
write_db pico_cts.db

# Loading the created database in OpenROAD
read_db pico_cts.db

# Read netlist post CTS
read_verilog /openLANE_flow/designs/picorv32a/runs/24-03_10-03/results/synthesis/picorv32a.synthesis_cts.v

# Read library for design
read_liberty $::env(LIB_SYNTH_COMPLETE)

# Link design and library
link_design picorv32a

# Read in the custom sdc we created
read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc

# Setting all cloks as propagated clocks
set_propagated_clock [all_clocks]

# Check syntax of 'report_checks' command
help report_checks

# Generating custom timing report
report_checks -path_delay min_max -fields {slew trans net cap input_pins} -format full_clock_expanded -digits 4

# Exit to OpenLANE flow
exit
```

Screenshots of commands run and timing report generated

![image](https://github.com/user-attachments/assets/56f53529-b13e-4d53-8930-e1ab830da06b)

![image](https://github.com/user-attachments/assets/356d8176-fbc7-4012-8fe8-17207e593f02)

![image](https://github.com/user-attachments/assets/7816b0c0-7f96-464d-bceb-58e0b467dcc7)

![image](https://github.com/user-attachments/assets/0b6f365e-3361-4c27-8460-79fed359af02)

#### 13. Explore post-CTS OpenROAD timing analysis by removing 'sky130_fd_sc_hd__clkbuf_1' cell from clock buffer list variable 'CTS_CLK_BUFFER_LIST'.

Commands to be run in OpenLANE flow to do OpenROAD timing analysis after changing `CTS_CLK_BUFFER_LIST`

```tcl
# Checking current value of 'CTS_CLK_BUFFER_LIST'
echo $::env(CTS_CLK_BUFFER_LIST)

# Removing 'sky130_fd_sc_hd__clkbuf_1' from the list
set ::env(CTS_CLK_BUFFER_LIST) [lreplace $::env(CTS_CLK_BUFFER_LIST) 0 0]

# Checking current value of 'CTS_CLK_BUFFER_LIST'
echo $::env(CTS_CLK_BUFFER_LIST)

# Checking current value of 'CURRENT_DEF'
echo $::env(CURRENT_DEF)

# Setting def as placement def
set ::env(CURRENT_DEF) /openLANE_flow/designs/picorv32a/runs/24-03_10-03/results/placement/picorv32a.placement.def

# Run CTS again
run_cts

# Checking current value of 'CTS_CLK_BUFFER_LIST'
echo $::env(CTS_CLK_BUFFER_LIST)

# Command to run OpenROAD tool
openroad

# Reading lef file
read_lef /openLANE_flow/designs/picorv32a/runs/24-03_10-03/tmp/merged.lef

# Reading def file
read_def /openLANE_flow/designs/picorv32a/runs/24-03_10-03/results/cts/picorv32a.cts.def

# Creating an OpenROAD database to work with
write_db pico_cts1.db

# Loading the created database in OpenROAD
read_db pico_cts.db

# Read netlist post CTS
read_verilog /openLANE_flow/designs/picorv32a/runs/24-03_10-03/results/synthesis/picorv32a.synthesis_cts.v

# Read library for design
read_liberty $::env(LIB_SYNTH_COMPLETE)

# Link design and library
link_design picorv32a

# Read in the custom sdc we created
read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc

# Setting all cloks as propagated clocks
set_propagated_clock [all_clocks]

# Generating custom timing report
report_checks -path_delay min_max -fields {slew trans net cap input_pins} -format full_clock_expanded -digits 4

# Report hold skew
report_clock_skew -hold

# Report setup skew
report_clock_skew -setup

# Exit to OpenLANE flow
exit

# Checking current value of 'CTS_CLK_BUFFER_LIST'
echo $::env(CTS_CLK_BUFFER_LIST)

# Inserting 'sky130_fd_sc_hd__clkbuf_1' to first index of list
set ::env(CTS_CLK_BUFFER_LIST) [linsert $::env(CTS_CLK_BUFFER_LIST) 0 sky130_fd_sc_hd__clkbuf_1]

# Checking current value of 'CTS_CLK_BUFFER_LIST'
echo $::env(CTS_CLK_BUFFER_LIST)
```

Screenshots of commands run and timing report generated

![image](https://github.com/user-attachments/assets/72c87bcd-e8c0-4786-af9e-89af6ddf0560)

![image](https://github.com/user-attachments/assets/2d0be52c-6217-4c7a-8a45-c188ab11cbcd)

![image](https://github.com/user-attachments/assets/87de62f5-51fe-4108-aa2b-6ec347f46771)

![image](https://github.com/user-attachments/assets/a89463a7-e6c6-47ed-a79d-3c218c9a2bdb)

![image](https://github.com/user-attachments/assets/e88ee844-d6e0-467b-9936-3ba76fb4b0b4)


Day 5:-

### Theory

### Implementation

* Section 5 tasks:-
1. Perform generation of Power Distribution Network (PDN) and explore the PDN layout.
2. Perfrom detailed routing using TritonRoute.
3. Post-Route parasitic extraction using SPEF extractor.
4. Post-Route OpenSTA timing analysis with the extracted parasitics of the route.

* All section 5 logs, reports and results can be found in following run folder:

[Section 5 Run - 26-03_08-45](https://github.com/fayizferosh/soc-design-and-planning-nasscom-vsd/tree/main/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/26-03_08-45)

#### 1. Perform generation of Power Distribution Network (PDN) and explore the PDN layout.

Commands to perform all necessary stages up until now

```bash
# Change directory to openlane flow directory
cd Desktop/work/tools/openlane_working_dir/openlane

# alias docker='docker run -it -v $(pwd):/openLANE_flow -v $PDK_ROOT:$PDK_ROOT -e PDK_ROOT=$PDK_ROOT -u $(id -u $USER):$(id -g $USER) efabless/openlane:v0.21'
# Since we have aliased the long command to 'docker' we can invoke the OpenLANE flow docker sub-system by just running this command
docker
```
```tcl
# Now that we have entered the OpenLANE flow contained docker sub-system we can invoke the OpenLANE flow in the Interactive mode using the following command
./flow.tcl -interactive

# Now that OpenLANE flow is open we have to input the required packages for proper functionality of the OpenLANE flow
package require openlane 0.9

# Now the OpenLANE flow is ready to run any design and initially we have to prep the design creating some necessary files and directories for running a specific design which in our case is 'picorv32a'
prep -design picorv32a

# Addiitional commands to include newly added lef to openlane flow merged.lef
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

# Command to set new value for SYNTH_STRATEGY
set ::env(SYNTH_STRATEGY) "DELAY 3"

# Command to set new value for SYNTH_SIZING
set ::env(SYNTH_SIZING) 1

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis

# Following commands are alltogather sourced in "run_floorplan" command
init_floorplan
place_io
tap_decap_or

# Now we are ready to run placement
run_placement

# Incase getting error
unset ::env(LIB_CTS)

# With placement done we are now ready to run CTS
run_cts

# Now that CTS is done we can do power distribution network
gen_pdn 
```

Screenshots of power distribution network run

![image](https://github.com/user-attachments/assets/1a62bfab-8939-4079-b25f-b294b8a2d2cc)

![image](https://github.com/user-attachments/assets/c34c91df-f889-429b-bdf0-9f1c5625628b)

![image](https://github.com/user-attachments/assets/792cad70-08af-454d-86c9-b3b333eeb42f)

![image](https://github.com/user-attachments/assets/21cd9fed-e344-4058-b32b-ec6023cf66b6)

![image](https://github.com/user-attachments/assets/26b15cc5-61bc-4312-be94-cad9a0597327)

![image](https://github.com/user-attachments/assets/c05a0dc3-f984-429c-8f24-4be5a8edb667)

![image](https://github.com/user-attachments/assets/a83300c3-65a3-4dec-a51d-fd64f30de878)

Commands to load PDN def in magic in another terminal

```bash
# Change directory to path containing generated PDN def
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/26-03_08-45/tmp/floorplan/

# Command to load the PDN def in magic tool
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read 14-pdn.def &
```

Screenshots of PDN def

![image](https://github.com/user-attachments/assets/6b26a54a-cbf9-4e4a-a63f-463bf40fea0d)

![image](https://github.com/user-attachments/assets/14461e75-f80e-477c-bdd1-f024cdb4ca27)

![image](https://github.com/user-attachments/assets/82422cf8-c612-4053-9679-ab2c9ec7afd2)

#### 2. Perfrom detailed routing using TritonRoute and explore the routed layout.

Command to perform routing

```tcl
# Check value of 'CURRENT_DEF'
echo $::env(CURRENT_DEF)

# Check value of 'ROUTING_STRATEGY'
echo $::env(ROUTING_STRATEGY)

# Command for detailed route using TritonRoute
run_routing
```

Screenshots of routing run

![image](https://github.com/user-attachments/assets/933e550f-876e-4081-88ea-8bb229faf06a)

![image](https://github.com/user-attachments/assets/c09847c0-5ac7-4053-8c07-0d3ff51bce88)

![image](https://github.com/user-attachments/assets/45a8a54d-7b06-4eac-806a-977ac022ad0b)

Commands to load routed def in magic in another terminal

```bash
# Change directory to path containing routed def
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/14-11_16-05/results/routing/

# Command to load the routed def in magic tool
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.def &
```

Screenshots of routed def

![image](https://github.com/user-attachments/assets/7eb028e4-eeba-46ea-a8f4-dff18524cb9a)

![image](https://github.com/user-attachments/assets/77669d68-8bb6-441f-8e19-909baecf8e49)

![image](https://github.com/user-attachments/assets/fa6d857d-7073-464b-9c72-16c041577059)

Screenshot of fast route guide present in `openlane/designs/picorv32a/runs/14-11_16-05/tmp/routing` directory

![image](https://github.com/user-attachments/assets/4d068b87-f0c0-4773-bc75-91972d427da1)

#### 3. Post-Route OpenSTA timing analysis with the extracted parasitics of the route.

Commands to be run in OpenLANE flow to do OpenROAD timing analysis with integrated OpenSTA in OpenROAD

```tcl
# Command to run OpenROAD tool
openroad

# Reading lef file
read_lef /openLANE_flow/designs/picorv32a/runs/26-03_08-45/tmp/merged.lef

# Reading def file
read_def /openLANE_flow/designs/picorv32a/runs/26-03_08-45/results/routing/picorv32a.def

# Creating an OpenROAD database to work with
write_db pico_route.db

# Loading the created database in OpenROAD
read_db pico_route.db

# Read netlist post CTS
read_verilog /openLANE_flow/designs/picorv32a/runs/26-03_08-45/results/synthesis/picorv32a.synthesis_preroute.v

# Read library for design
read_liberty $::env(LIB_SYNTH_COMPLETE)

# Link design and library
link_design picorv32a

# Read in the custom sdc we created
read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc

# Setting all cloks as propagated clocks
set_propagated_clock [all_clocks]

# Read SPEF
read_spef /openLANE_flow/designs/picorv32a/runs/26-03_08-45/results/routing/picorv32a.spef

# Generating custom timing report
report_checks -path_delay min_max -fields {slew trans net cap input_pins} -format full_clock_expanded -digits 4

# Exit to OpenLANE flow
exit
```

Screenshots of commands run and timing report generated

![image](https://github.com/user-attachments/assets/2e72fecd-434b-4c7e-9275-5c893e27044e)

![image](https://github.com/user-attachments/assets/44c7db06-2ae3-463c-88f8-b1316b429c4f)

![image](https://github.com/user-attachments/assets/5ca89b15-bb4f-4027-925f-8eeeb047aa2e)

![image](https://github.com/user-attachments/assets/c494cfb5-8419-46a3-b3cb-e3b6e47ba75c)



</details>

<details>
	<summary> Assignment 14</summary>


 # OpenROAD and ORFS: A Complete RTL-to-GDSII Solution

OpenROAD is a state-of-the-art digital design tool that simplifies the ASIC development process by offering a fully automated flow from RTL to GDSII. It integrates all stages of the physical design flow, including **synthesis, floorplanning, placement, routing, parasitic extraction, and timing analysis**. Designed for flexibility and scalability, OpenROAD employs a hierarchical placement algorithm to minimize wire length and optimize timing and power. Its modular architecture allows users to integrate custom algorithms and features easily.

The OpenROAD project provides two main flow controllers:

## OpenROAD-flow-scripts (ORFS)
ORFS is a comprehensive flow controller that automates the entire **RTL-to-GDSII** process. It integrates multiple open-source tools for key stages like synthesis, placement, routing, static timing analysis (STA), and layout verification. ORFS allows designers to:
- Perform **Synthesis**
- Conduct **Placement and Routing (PnR)**
- Perform **Static Timing Analysis (STA)**
- Check for **Design Rule Compliance (DRC)**
- Validate designs with **Layout Versus Schematic (LVS)**

Within ORFS, OpenROAD acts as a plugin during the physical design stages, providing advanced capabilities like **hierarchical placement**, **global routing**, and **detailed routing optimization**.

ORFS supports both public and private PDKs. Notable public PDKs include:
- **GF180**
- **SkyWater130**
- **ASAP7**

## OpenLane
OpenLane is another RTL-to-GDSII flow, developed by Efabless for the **SkyWater130 MPW Program**. It is similar to ORFS but specifically optimized for SkyWater130.

For additional details, visit the [OpenROAD Documentation](https://openroad.readthedocs.io/en/latest/main/README.html).

---

## ORFS Flow: From RTL to GDSII

The OpenROAD Flow Scripts (ORFS) simplifies the chip design process into the following stages:

### 1. Configuration
Customize ORFS for your design project by specifying key parameters such as:
- Target technology node
- Design constraints
- Tool settings

### 2. Design Entry
Input your design into ORFS using supported formats such as **Verilog**.

### 3. Synthesis
Transform the RTL design into a gate-level netlist using open-source synthesis tools like:
- **Yosys**
- **ABC**

### 4. Floorplanning
Define the placement of design modules within the chip area using tools like:
- **Replace**
- **Capo**

### 5. Placement
Determine the exact location of gates and cells using OpenROAD's robust placement capabilities.

### 6. Routing
Connect gates and cells with metal interconnects using routing tools like:
- **FastRoute**
- **TritonRoute**

### 7. Layout Verification
Verify the correctness of the layout using tools like **Magic** to ensure the design meets all requirements.

### 8. GDSII Generation
Generate the final GDSII layout file using tools like:
- **Magic**
- **KLayout**

This comprehensive flow ensures an efficient and streamlined path to generating a manufacturable chip layout.

---

## Key Features of OpenROAD and ORFS
- Fully automated **RTL-to-GDSII** flow
- Flexible and modular architecture for customizations
- Advanced optimizations for physical design
- Public PDK support: **GF180, SkyWater130, ASAP7**
- Comprehensive design verification, including DRC and LVS

---

 # Tool Installation

 The commands for tool installation are as follows:-

 ``` bash
git clone --recursive https://github.com/The-OpenROAD-Project/OpenROAD-flow-scripts
cd OpenROAD-flow-scripts
sudo ./setup.sh
```

![Screenshot from 2024-11-22 21-15-53](https://github.com/user-attachments/assets/acc4a27e-c72a-44ab-9a48-2254bffbe029)

![Screenshot from 2024-11-22 21-21-19](https://github.com/user-attachments/assets/35e4911b-000e-489c-85f5-0998acebbcfb)

```bash
sudo ./etc/DependencyInstaller.sh
```

![image](https://github.com/user-attachments/assets/0f2723b3-4446-4e07-9372-c4766542cb7f)


```bash
./build_openroad.sh --local
```

![Screenshot from 2024-11-22 21-27-41](https://github.com/user-attachments/assets/f4d38cc2-5269-4ea1-812b-7946f1fded00)


## ORFS Directory Structure

We observe the following files inside the folders created

![image](https://github.com/user-attachments/assets/0e7b5b99-ac34-49b1-b376-e305b924f8dd)

![image](https://github.com/user-attachments/assets/c8f3dac6-9098-44ae-ad44-87c86dad58e6)

- The designs library has different examples for RTL to GDS flow across different technology nodes.
- Platforms directory has different technology node libraries, lib files, GDS,etc. The ORFS automated flow has been defined inside the platforms directory

If we go inside the src directory we see all the built in designs and its corresponding verilog code. So in case we need to add a new code in the top module we will add that design in the source folder as shown below.

![image](https://github.com/user-attachments/assets/d04c15ac-881a-4b31-a49e-56b0a953a0a3)


Since we want to work with nandgate45 design we go into the following directory


![image](https://github.com/user-attachments/assets/21a2382c-28c7-493d-b86d-3cd35c53ffa9)

To understand what variables are inside we go inside the following file

![image](https://github.com/user-attachments/assets/3b6946f4-4725-4b4c-9f1e-2b9bd321ae61)

The variables are as follows:-

![image](https://github.com/user-attachments/assets/1f64951d-4df7-4845-8f43-948575eadd1a)

If there are multiple design files which we need to use we need to add them in these files a shown in the below examples

![image](https://github.com/user-attachments/assets/2df523ca-43af-41d2-9517-b569d6505235)


## Steps to include constraints file

For the microwatt example in the designs directory we oberve the following constraints.sdc file

![image](https://github.com/user-attachments/assets/b9aa442b-3b59-4c81-a363-6d58f69415c8)

![image](https://github.com/user-attachments/assets/e1116e65-5fc1-41ec-8461-e0423b27f0be)


For our own project we can replace the .sdc file based on our requirements

## Default config file setup

We have the following publicly available pdk files

![image](https://github.com/user-attachments/assets/132649f6-74e5-44a5-ba3a-d8f24fa87780)

We have the following files and directories in the nandgate pdk

![image](https://github.com/user-attachments/assets/cdd11594-41ea-4df3-8f23-e6a52163275e)

The config file is as follows:-

![image](https://github.com/user-attachments/assets/f13e44ab-6c02-4214-a8e1-a172954246de)

## Default Openroad flow using make command

The make command runs the entire RTL to GDS flow

![image](https://github.com/user-attachments/assets/c711d9de-8ba2-4074-a02d-850426af2442)

Afte running the make command we can now see the logs, objects , reports and results folder as shown below

![image](https://github.com/user-attachments/assets/16499e13-3d92-4fcd-bb65-a826988b70b9)

The whole execution can be seen as follows:-

![image](https://github.com/user-attachments/assets/a8b309a0-7d0b-41a4-802a-222c98aca79d)

![image](https://github.com/user-attachments/assets/54e79827-1eff-433f-82ed-bfcd3dfc244e)

![image](https://github.com/user-attachments/assets/ee2b8177-63c9-4243-b164-e376640f06b3)

![image](https://github.com/user-attachments/assets/53b95940-9a4b-45d6-983d-127716dbd7b9)

![image](https://github.com/user-attachments/assets/2fdaa551-d40d-4471-82a5-a3e42cd96bc9)

![image](https://github.com/user-attachments/assets/e41186a0-f7c2-42ec-82ab-bf874abe64c5)

![image](https://github.com/user-attachments/assets/194f2962-b287-42c6-9566-604f2c182984)

We also have the option to run individual stages instead of running the entire RTL to GDS flow by using the following command

```bash
make DESIGN_CONFIG=./designs/sky130hd/gcd/config.mk synth
make DESIGN_CONFIG=./designs/sky130hd/gcd/config.mk floorplan
```
The above command is to run synthesis stage and the floorplan stage

![image](https://github.com/user-attachments/assets/2be2a564-883f-4cfa-ac56-f9f5c832f08b)

![image](https://github.com/user-attachments/assets/afe86feb-4e1e-4644-9035-f6051327c4ec)



## OpenROAD GUI And Review Logs For Synthesis, Floorplan and Init STA

We use the below command and get the following result to observe the floorplanning

```bash
make gui_floorplan
```

![image](https://github.com/user-attachments/assets/089e14dd-6aca-4ebb-8713-be1abb034b26)

The command to see the floorplanning is as follows and we get the following layout

```
make DESIGN_CONFIG=./designs/sky130hd/gcd/config.mk gui_floorplan
```

In order to read the log files we go through the following commands

![image](https://github.com/user-attachments/assets/1f70f0a7-5275-4f92-90fd-9f138c5f8e44)

![image](https://github.com/user-attachments/assets/f4f03c21-305c-47f2-97ac-24f65a6926af)

We also have the floorplan, place and the pdn files as shown below

![image](https://github.com/user-attachments/assets/8ffdb708-1830-4dbe-9edf-90545b826952)


Based on the availability of the metals the grid strategy varies and we can refer to this in the following file

![image](https://github.com/user-attachments/assets/28ee0bfa-9c8e-4475-8e41-93151e26087b)

In order to observe the slack values we go through the floorplan.log file

## Review Logs For Placement CTS And Routing

- The cts.log files can be analysed to meet the slew requirements.
- In the routing stage we have the fastroute and the Tritenroute.log files. They are used to fix the routing violations found in the design.

![image](https://github.com/user-attachments/assets/6db54b2b-e122-4bd8-8605-83a02f662b08)

![image](https://github.com/user-attachments/assets/c1adb985-d1f3-4f7b-a92f-cfeb391650ae)

The detailed routing file is as  follows:-

![image](https://github.com/user-attachments/assets/7249b30d-8d2e-4f4a-af41-8ea6e84a73f0)

The merge file is as follows:-

![image](https://github.com/user-attachments/assets/d83cef61-1245-417e-b181-bc283c07f8e9)

## Final Checks

The final report.log file is as follows:-

![image](https://github.com/user-attachments/assets/1291ef82-7946-4aa3-8d2c-66fac9df006c)

In order to view all the files in the RTL to GDS flow we go to the following directory

```bash
gvim reports/nangate45/gcd/base/synth_stat.txt
```

The synthesis statistics is as follows

![image](https://github.com/user-attachments/assets/d168dcbf-8312-43ed-ab6a-fe97b7166139)


# Openroad GUI

## GUI Overview And Floorplan GUI Details

There are two ways to open the GUI. The commands are as follows:-

```bash
make gui_floorplan
```

We get the following GUI

![image](https://github.com/user-attachments/assets/cb6d63e7-86ae-4d57-82a1-f42ee057eaae)

Another way of opening the GUI is as follows:-

```bash
openroad -gui
```

![image](https://github.com/user-attachments/assets/9d1afb76-763c-4cc8-8222-40bbcd7efcc9)


After this go and select the file which you want to open

Similar to this we can see the placement of the design by using the following command

```bash
make gui_place
```

![image](https://github.com/user-attachments/assets/6e31e3e5-eb82-46f9-8ec9-3b5e0e6d4355)


For clock tree synthesis we use the following command
```bash
make gui_cts
```

![image](https://github.com/user-attachments/assets/1049d394-cc31-4a7c-bcb8-d652fee28e80)

For routing the commands are

```bash
make gui_route
```

![image](https://github.com/user-attachments/assets/0081653f-c782-43ce-9334-94767844c1cb)

For the final layout

```bash
make gui_final
```

![image](https://github.com/user-attachments/assets/4d980906-7c4e-4c48-946b-7570d1f4d29d)

The executed commands are as follows:-

![image](https://github.com/user-attachments/assets/2caffa8f-0fae-4bc0-bfe0-96d1f2116352)

Similar to these flow of operations we just need to make changes in the makefile and uncomment the design file which for which we want to observe the layout

## CTS GUI Heatmaps

In the placement process, we analyze the cell density in the layout using heatmaps. Below are the heatmaps displayed in a grid layout for better visualization:

<table>
  <tr>
	<td align="center">
  	<img src="https://github.com/user-attachments/assets/533c279d-2541-4893-8377-5ea1a2fc0990" alt="Heatmap 1" width="300">
  	<br>Heatmap 1
	</td>
	<td align="center">
  	<img src="https://github.com/user-attachments/assets/05001d18-4c49-457b-bddb-4a086edb6b0b" alt="Heatmap 2" width="300">
  	<br>Heatmap 2
	</td>
  </tr>
  <tr>
	<td align="center">
  	<img src="https://github.com/user-attachments/assets/f32459a7-1555-4360-9ce3-17f937eefe3a" alt="Heatmap 3" width="300">
  	<br>Heatmap 3
	</td>
	<td align="center">
  	<img src="https://github.com/user-attachments/assets/e2991a9a-abde-4c1e-917b-33d7dae86685" alt="Heatmap 4" width="300">
  	<br>Heatmap 4
	</td>
  </tr>
  <tr>
	<td colspan="2" align="center">
  	<img src="https://github.com/user-attachments/assets/be4f067b-b46a-4dcd-a5d8-37347959e366" alt="Heatmap 5" width="400">
  	<br>Heatmap 5
	</td>
  </tr>
</table>


For clock tree synthesis use the following code

```bash
make gui_cts
```
![image](https://github.com/user-attachments/assets/c27fcbed-b36e-4155-a7cb-ad8c2b84f656)

The timing report option gives us the setup and the hold slack. We have multiple paths so we can select any particular path in the design and get the capture path and the data path details


## Detailed Route, Heat Map And Metal Fillers GUI Details

The routing congestion graph is as follows:-

![image](https://github.com/user-attachments/assets/331e6834-6b3b-4dea-a1b7-9d77b0605964)

The final layout of the file is as follows:-

![image](https://github.com/user-attachments/assets/508e6794-c268-429d-adf2-680913057fc6)

We can also observe the timing report for both the setup and the hold values

![image](https://github.com/user-attachments/assets/0ebc7d5c-d0ac-4249-9905-c7179cd8c732)

![image](https://github.com/user-attachments/assets/098736b3-b58f-417c-9aff-9658a3bec06f)

To give the GDS file in the klayout type the following commands

```bash
 klayout -e -nn ./platforms/nangate45/FreePDK45.lyt -l ./platforms/nangate45/FreePDK45.lyp ./results/nangate45/gcd/base/6_final.gds
```

![image](https://github.com/user-attachments/assets/dc9d3c21-33db-4e91-bf92-96e1c7a82022)


![image](https://github.com/user-attachments/assets/84a165b4-650c-41bb-9e33-c5eaea0f93b8)

# Macro Placement RTL MP And QOR

## Config Setup For Macro Placement

We are going to do the macro placement for the following file

![image](https://github.com/user-attachments/assets/8b318ba1-e578-476c-a469-68fe804b3dc5)

We use the following file

![image](https://github.com/user-attachments/assets/22df5d15-3053-46e4-99a4-62e176cda144)


![image](https://github.com/user-attachments/assets/10844da5-f578-4a66-b8bf-d32452f6ac44)


## Steps To Run And Review Macro Placement

We need to uncomment this line in the make file

![image](https://github.com/user-attachments/assets/6d3955b4-a103-47ff-99a4-bbcafbd9088d)


![image](https://github.com/user-attachments/assets/b7ce51d6-fe5b-436e-a89d-e33bd21ff43f)


After this step we use the make command and run the design for the floorplan step nad get the layout

![image](https://github.com/user-attachments/assets/07ae9948-080b-40aa-b1aa-c5c37fc5ecdd)


## QOR checking

We need a golden reference with which we can compare our data. In the above example we are using the below file

We use the following command to check whether or not we are able to satisfy all the design checks

```bash
make metadata
```

![image](https://github.com/user-attachments/assets/60d69007-f2f1-4aff-bb59-7607a9cba0e8)


```bash
gvim designs/nangate45/gcd/metadata-base-ok.json
```
![image](https://github.com/user-attachments/assets/d9624ed8-e6f8-43c1-8210-515e46d838eb)

# Design Exploration Using Autotuner

## Autotuner Overview And Pre-requisites Packages

Autotuner is a ML based design exploration tool. It is essential for optimizing PPA ( Performance, Power and Area ) parameters in the circuit.

![image](https://github.com/user-attachments/assets/2fe31ae7-6395-4665-b6a1-9cd36a2b35e4)

We have the above fixed configuration variables from which we are allowed to change on the min and max values and we will observe the result of this change in the design


## Steps To Run Autotuner

Tool Installation:-

``` bash
pip3.9 install -U --user 'ray[default,tue]==1.11.0' ax-platform hyperopt nevergrad optuna pandas
pip3.9 install -U --user colorama==0.4.4 bayesian-optimization==1.4.0
```
Commands to run Autotuner

```bash

python3.9 distributed.py --design gcd --platform sky130hd \
                   	--config ../../../../flow/designs/sky130hd/gcd/autotuner.json \
                   	tune
```


![image](https://github.com/user-attachments/assets/3e4cbf6c-55e3-4b33-ac22-74d9eb1b48cf)

The autotuner.json file is as follows:-

![image](https://github.com/user-attachments/assets/58efae72-a7e4-4fa5-b84c-065244a61644)



After running the autotuner we get the best parameters found for our given set of values.

We then use the following command to open tensorboard

```bash
tensorboard --logdir=../logs/sky130hd/gcd/teset-tune-2024-25-09-11-31-33/
```
![image](https://github.com/user-attachments/assets/d5ddbcd3-7b15-47c7-af88-0b9f78263076)

The green path obtained indicates the most optimum configuration for our design.

# Execution with VSDBabysoc

## Synthesis

We first have to copy the folders and the files in the respective locations as mentioned in the below config.mk file

I have created a vsdbabysoc folder in the src and the platforms directory. After this I have added the gds, include ,lef and lib folder in the above two folders.


The following command was used to run synthesis:-

```bash
make DESIGN_CONFIG=./designs/sky130hd/vsdbabysoc/config.mk synth
```

![image](https://github.com/user-attachments/assets/570f9827-d777-4d87-b272-b267bf7cfa2a)

The config.mk file is as follows:-

```bash
export DESIGN_NICKNAME = vsdbabysoc
export DESIGN_NAME = vsdbabysoc
export PLATFORM	= sky130hd

export VERILOG_FILES = $(DESIGN_HOME)/src/$(DESIGN_NICKNAME)/vsdbabysoc.v \
           	$(DESIGN_HOME)/src/$(DESIGN_NICKNAME)/rvmyth.v \
           	$(DESIGN_HOME)/src/$(DESIGN_NICKNAME)/clk_gate.v
        	 
export ADDITIONAL_LIBS = $(DESIGN_HOME)/src/$(DESIGN_NICKNAME)/lib/avsddac.lib \
             	$(DESIGN_HOME)/src/$(DESIGN_NICKNAME)/lib/avsdpll.lib

export VERILOG_INCLUDE_DIRS = $(DESIGN_HOME)/src/$(DESIGN_NICKNAME)/include

export SDC_FILE  	=   $(DESIGN_HOME)/$(PLATFORM)/$(DESIGN_NICKNAME)/vsdbabysoc_synthesis.sdc

export ADDITIONAL_LEFS = $(DESIGN_HOME)/src/$(DESIGN_NICKNAME)/lef/avsddac.lef \
          	$(DESIGN_HOME)/src/$(DESIGN_NICKNAME)/lef/avsdpll.lef


export ADDITIONAL_GDS = $(DESIGN_HOME)/src/$(DESIGN_NICKNAME)/gds/avsddac.gds \
        	$(DESIGN_HOME)/src/$(DESIGN_NICKNAME)/gds/avsdpll.gds

#export PDN_TCL = $(DESIGN_HOME)/$(PLATFORM)/$(DESIGN_NICKNAME)/pdn.tcl

export DIE_AREA   = 0 0 1600 1600
export CORE_AREA  = 20 20 1590 1590

export PLACE_PINS_ARGS = -exclude left:0-600 -exclude left:1000-1600: -exclude right:* -exclude top:* -exclude bottom:*
export MACRO_PLACEMENT = $(DESIGN_HOME)/$(PLATFORM)/$(DESIGN_NICKNAME)/macro_placement.cfg

export TNS_END_PERCENT = 100

export REMOVE_ABC_BUFFERS = 1
```

The following commands were executed on terminal

![image](https://github.com/user-attachments/assets/fe585fdf-35a4-473f-be19-4d7f5d8355a1)


## Floorplanning

```bash
make DESIGN_CONFIG=./designs/sky130hd/vsdbabysoc/config.mk floorplan
```
![image](https://github.com/user-attachments/assets/0517889a-3708-415c-9aa5-d0c45b105995)


In order to see the GUI we run the following command

```bash
make gui_floorplan
```

![image](https://github.com/user-attachments/assets/3ddb9ad3-9ee4-4161-bc7d-c9fa32092161)

### Heatmaps

![image](https://github.com/user-attachments/assets/53698a1e-603c-4216-9eae-e5f564010e40)

![image](https://github.com/user-attachments/assets/23f09f61-7353-4a75-88b8-33d45a320069)

![image](https://github.com/user-attachments/assets/c9f5ba2e-1bb4-4dc5-8380-789cd9d754ae)

![image](https://github.com/user-attachments/assets/4fc3c335-71b7-4b3d-842e-3a8b37d321d7)

![image](https://github.com/user-attachments/assets/77a9b1d1-ddde-4471-bbc0-bf33b81ca2bc)


### Floorplanning report

```bash


==========================================================================
floorplan final report_tns
--------------------------------------------------------------------------
tns -812.19

==========================================================================
floorplan final report_wns
--------------------------------------------------------------------------
wns -3.36

==========================================================================
floorplan final report_worst_slack
--------------------------------------------------------------------------
worst slack -3.36

==========================================================================
floorplan final report_checks -path_delay min
--------------------------------------------------------------------------
Startpoint: core.CPU_imm_a2[11]$_DFF_P_
            (rising edge-triggered flip-flop clocked by clk)
Endpoint: core.CPU_imm_a3[11]$_DFF_P_
          (rising edge-triggered flip-flop clocked by clk)
Path Group: clk
Path Type: min

Fanout     Cap    Slew   Delay    Time   Description
-----------------------------------------------------------------------------
                  0.00    0.00    0.00   clock clk (rise edge)
                          0.00    0.00   clock network delay (ideal)
                  0.00    0.00    0.00 ^ core.CPU_imm_a2[11]$_DFF_P_/CLK (sky130_fd_sc_hd__dfxtp_1)
     1    0.00    0.03    0.27    0.27 ^ core.CPU_imm_a2[11]$_DFF_P_/Q (sky130_fd_sc_hd__dfxtp_1)
                                         core.CPU_imm_a2[11] (net)
                  0.03    0.00    0.27 ^ core.CPU_imm_a3[11]$_DFF_P_/D (sky130_fd_sc_hd__dfxtp_1)
                                  0.27   data arrival time

                  0.00    0.00    0.00   clock clk (rise edge)
                          0.00    0.00   clock network delay (ideal)
                          0.00    0.00   clock reconvergence pessimism
                                  0.00 ^ core.CPU_imm_a3[11]$_DFF_P_/CLK (sky130_fd_sc_hd__dfxtp_1)
                         -0.03   -0.03   library hold time
                                 -0.03   data required time
-----------------------------------------------------------------------------
                                 -0.03   data required time
                                 -0.27   data arrival time
-----------------------------------------------------------------------------
                                  0.31   slack (MET)



==========================================================================
floorplan final report_checks -path_delay max
--------------------------------------------------------------------------
Startpoint: core.CPU_reset_a3$_DFF_P_
            (rising edge-triggered flip-flop clocked by clk)
Endpoint: core.CPU_Xreg_value_a4[11][26]$_SDFFE_PP0P_
          (rising edge-triggered flip-flop clocked by clk)
Path Group: clk
Path Type: max

Fanout     Cap    Slew   Delay    Time   Description
-----------------------------------------------------------------------------
                  0.00    0.00    0.00   clock clk (rise edge)
                          0.00    0.00   clock network delay (ideal)
                  0.00    0.00    0.00 ^ core.CPU_reset_a3$_DFF_P_/CLK (sky130_fd_sc_hd__dfxtp_1)
   256    0.64    5.89    4.39    4.39 ^ core.CPU_reset_a3$_DFF_P_/Q (sky130_fd_sc_hd__dfxtp_1)
                                         core.CPU_reset_a3 (net)
                  5.89    0.00    4.39 ^ _08000_/A (sky130_fd_sc_hd__inv_1)
   283    0.65    1.13    7.27   11.66 v _08000_/Y (sky130_fd_sc_hd__inv_1)
                                         _02630_ (net)
                  1.13    0.00   11.66 v _08421_/B1 (sky130_fd_sc_hd__o21ai_1)
    15    0.04    0.76    0.89   12.55 ^ _08421_/Y (sky130_fd_sc_hd__o21ai_1)
                                         _03034_ (net)
                  0.76    0.00   12.55 ^ _08720_/A2 (sky130_fd_sc_hd__o31ai_1)
     1    0.00    0.17    0.13   12.68 v _08720_/Y (sky130_fd_sc_hd__o31ai_1)
                                         _00594_ (net)
                  0.17    0.00   12.68 v core.CPU_Xreg_value_a4[11][26]$_SDFFE_PP0P_/D (sky130_fd_sc_hd__dfxtp_1)
                                 12.68   data arrival time

                  0.00    9.50    9.50   clock clk (rise edge)
                          0.00    9.50   clock network delay (ideal)
                          0.00    9.50   clock reconvergence pessimism
                                  9.50 ^ core.CPU_Xreg_value_a4[11][26]$_SDFFE_PP0P_/CLK (sky130_fd_sc_hd__dfxtp_1)
                         -0.18    9.32   library setup time
                                  9.32   data required time
-----------------------------------------------------------------------------
                                  9.32   data required time
                                -12.68   data arrival time
-----------------------------------------------------------------------------
                                 -3.36   slack (VIOLATED)



==========================================================================
floorplan final report_checks -unconstrained
--------------------------------------------------------------------------
Startpoint: core.CPU_reset_a3$_DFF_P_
            (rising edge-triggered flip-flop clocked by clk)
Endpoint: core.CPU_Xreg_value_a4[11][26]$_SDFFE_PP0P_
          (rising edge-triggered flip-flop clocked by clk)
Path Group: clk
Path Type: max

Fanout     Cap    Slew   Delay    Time   Description
-----------------------------------------------------------------------------
                  0.00    0.00    0.00   clock clk (rise edge)
                          0.00    0.00   clock network delay (ideal)
                  0.00    0.00    0.00 ^ core.CPU_reset_a3$_DFF_P_/CLK (sky130_fd_sc_hd__dfxtp_1)
   256    0.64    5.89    4.39    4.39 ^ core.CPU_reset_a3$_DFF_P_/Q (sky130_fd_sc_hd__dfxtp_1)
                                         core.CPU_reset_a3 (net)
                  5.89    0.00    4.39 ^ _08000_/A (sky130_fd_sc_hd__inv_1)
   283    0.65    1.13    7.27   11.66 v _08000_/Y (sky130_fd_sc_hd__inv_1)
                                         _02630_ (net)
                  1.13    0.00   11.66 v _08421_/B1 (sky130_fd_sc_hd__o21ai_1)
    15    0.04    0.76    0.89   12.55 ^ _08421_/Y (sky130_fd_sc_hd__o21ai_1)
                                         _03034_ (net)
                  0.76    0.00   12.55 ^ _08720_/A2 (sky130_fd_sc_hd__o31ai_1)
     1    0.00    0.17    0.13   12.68 v _08720_/Y (sky130_fd_sc_hd__o31ai_1)
                                         _00594_ (net)
                  0.17    0.00   12.68 v core.CPU_Xreg_value_a4[11][26]$_SDFFE_PP0P_/D (sky130_fd_sc_hd__dfxtp_1)
                                 12.68   data arrival time

                  0.00    9.50    9.50   clock clk (rise edge)
                          0.00    9.50   clock network delay (ideal)
                          0.00    9.50   clock reconvergence pessimism
                                  9.50 ^ core.CPU_Xreg_value_a4[11][26]$_SDFFE_PP0P_/CLK (sky130_fd_sc_hd__dfxtp_1)
                         -0.18    9.32   library setup time
                                  9.32   data required time
-----------------------------------------------------------------------------
                                  9.32   data required time
                                -12.68   data arrival time
-----------------------------------------------------------------------------
                                 -3.36   slack (VIOLATED)



==========================================================================
floorplan final report_power
--------------------------------------------------------------------------
Group                  Internal  Switching    Leakage      Total
                          Power      Power      Power      Power (Watts)
----------------------------------------------------------------
Sequential             5.93e-03   3.61e-04   1.03e-08   6.29e-03  72.2%
Combinational          9.93e-04   1.43e-03   8.24e-09   2.42e-03  27.8%
Clock                  0.00e+00   0.00e+00   0.00e+00   0.00e+00   0.0%
Macro                  0.00e+00   0.00e+00   0.00e+00   0.00e+00   0.0%
Pad                    0.00e+00   0.00e+00   0.00e+00   0.00e+00   0.0%
----------------------------------------------------------------
Total                  6.92e-03   1.79e-03   1.86e-08   8.71e-03 100.0%
                          79.5%      20.5%       0.0%
```



We get the following layout

![image](https://github.com/user-attachments/assets/9060109e-aabc-4d01-8326-c33d3e4967d4)

![image](https://github.com/user-attachments/assets/36fcf6ed-07b2-4769-979e-56e94966b413)

![image](https://github.com/user-attachments/assets/669c9eea-a139-49a7-9361-3a79e45a43bd)

### PLL

![image](https://github.com/user-attachments/assets/4b0f0114-8f6e-4da9-9b47-6e4ce469f7ae)

### DAC

![image](https://github.com/user-attachments/assets/c5e31049-b89d-4f72-aa7b-bdbb287aef33)

## Placement

![image](https://github.com/user-attachments/assets/07fecc90-f3c5-44bb-9c2b-dd7a45e85f84)


![image](https://github.com/user-attachments/assets/686e596d-6a7f-4fab-b6c0-3dd2b3bb0873)

### Placement report

```bash

==========================================================================
detailed place report_tns
--------------------------------------------------------------------------
tns 0.00

==========================================================================
detailed place report_wns
--------------------------------------------------------------------------
wns 0.00

==========================================================================
detailed place report_worst_slack
--------------------------------------------------------------------------
worst slack 5.11

==========================================================================
detailed place report_checks -path_delay min
--------------------------------------------------------------------------
Startpoint: core.CPU_imm_a2[11]$_DFF_P_
            (rising edge-triggered flip-flop clocked by clk)
Endpoint: core.CPU_imm_a3[11]$_DFF_P_
          (rising edge-triggered flip-flop clocked by clk)
Path Group: clk
Path Type: min

Fanout     Cap    Slew   Delay    Time   Description
-----------------------------------------------------------------------------
                  0.00    0.00    0.00   clock clk (rise edge)
                          0.00    0.00   clock network delay (ideal)
                  0.00    0.00    0.00 ^ core.CPU_imm_a2[11]$_DFF_P_/CLK (sky130_fd_sc_hd__dfxtp_1)
     1    0.00    0.04    0.28    0.28 ^ core.CPU_imm_a2[11]$_DFF_P_/Q (sky130_fd_sc_hd__dfxtp_1)
                                         core.CPU_imm_a2[11] (net)
                  0.04    0.00    0.28 ^ core.CPU_imm_a3[11]$_DFF_P_/D (sky130_fd_sc_hd__dfxtp_2)
                                  0.28   data arrival time

                  0.00    0.00    0.00   clock clk (rise edge)
                          0.00    0.00   clock network delay (ideal)
                          0.00    0.00   clock reconvergence pessimism
                                  0.00 ^ core.CPU_imm_a3[11]$_DFF_P_/CLK (sky130_fd_sc_hd__dfxtp_2)
                         -0.04   -0.04   library hold time
                                 -0.04   data required time
-----------------------------------------------------------------------------
                                 -0.04   data required time
                                 -0.28   data arrival time
-----------------------------------------------------------------------------
                                  0.31   slack (MET)



==========================================================================
detailed place report_checks -path_delay max
--------------------------------------------------------------------------
Startpoint: core.CPU_valid_load_a5$_DFF_P_
            (rising edge-triggered flip-flop clocked by clk)
Endpoint: core.CPU_Xreg_value_a4[14][18]$_SDFFE_PP0P_
          (rising edge-triggered flip-flop clocked by clk)
Path Group: clk
Path Type: max

Fanout     Cap    Slew   Delay    Time   Description
-----------------------------------------------------------------------------
                  0.00    0.00    0.00   clock clk (rise edge)
                          0.00    0.00   clock network delay (ideal)
                  0.00    0.00    0.00 ^ core.CPU_valid_load_a5$_DFF_P_/CLK (sky130_fd_sc_hd__dfxtp_1)
     2    0.02    0.15    0.36    0.36 ^ core.CPU_valid_load_a5$_DFF_P_/Q (sky130_fd_sc_hd__dfxtp_1)
                                         core.CPU_valid_load_a5 (net)
                  0.15    0.00    0.36 ^ _05805_/D (sky130_fd_sc_hd__or4_4)
    48    0.47    1.32    1.04    1.41 ^ _05805_/X (sky130_fd_sc_hd__or4_4)
                                         _01035_ (net)
                  1.32    0.01    1.42 ^ _05806_/A (sky130_fd_sc_hd__clkinv_16)
    48    0.45    0.53    0.56    1.98 v _05806_/Y (sky130_fd_sc_hd__clkinv_16)
                                         _01036_ (net)
                  0.53    0.01    1.99 v _07859_/C (sky130_fd_sc_hd__nor3_1)
     1    0.01    0.27    0.35    2.35 ^ _07859_/Y (sky130_fd_sc_hd__nor3_1)
                                         _02490_ (net)
                  0.27    0.00    2.35 ^ _07860_/B1 (sky130_fd_sc_hd__a21oi_2)
     3    0.02    0.14    0.12    2.47 v _07860_/Y (sky130_fd_sc_hd__a21oi_2)
                                         _02491_ (net)
                  0.14    0.00    2.47 v _07956_/B (sky130_fd_sc_hd__nor3_4)
     4    0.08    0.77    0.67    3.14 ^ _07956_/Y (sky130_fd_sc_hd__nor3_4)
                                         _02586_ (net)
                  0.77    0.00    3.14 ^ _08969_/A (sky130_fd_sc_hd__nand2_8)
    49    0.27    0.43    0.48    3.62 v _08969_/Y (sky130_fd_sc_hd__nand2_8)
                                         _03467_ (net)
                  0.43    0.02    3.64 v _08993_/B (sky130_fd_sc_hd__nor2_2)
     5    0.03    0.32    0.40    4.04 ^ _08993_/Y (sky130_fd_sc_hd__nor2_2)
                                         _03483_ (net)
                  0.32    0.00    4.04 ^ _08994_/B1 (sky130_fd_sc_hd__o21ai_0)
     1    0.00    0.10    0.14    4.18 v _08994_/Y (sky130_fd_sc_hd__o21ai_0)
                                         _03484_ (net)
                  0.10    0.00    4.18 v _08997_/A1 (sky130_fd_sc_hd__a21oi_1)
     1    0.00    0.10    0.13    4.32 ^ _08997_/Y (sky130_fd_sc_hd__a21oi_1)
                                         _00681_ (net)
                  0.10    0.00    4.32 ^ core.CPU_Xreg_value_a4[14][18]$_SDFFE_PP0P_/D (sky130_fd_sc_hd__dfxtp_1)
                                  4.32   data arrival time

                  0.00    9.50    9.50   clock clk (rise edge)
                          0.00    9.50   clock network delay (ideal)
                          0.00    9.50   clock reconvergence pessimism
                                  9.50 ^ core.CPU_Xreg_value_a4[14][18]$_SDFFE_PP0P_/CLK (sky130_fd_sc_hd__dfxtp_1)
                         -0.07    9.43   library setup time
                                  9.43   data required time
-----------------------------------------------------------------------------
                                  9.43   data required time
                                 -4.32   data arrival time
-----------------------------------------------------------------------------
                                  5.11   slack (MET)



==========================================================================
detailed place report_checks -unconstrained
--------------------------------------------------------------------------
Startpoint: core.CPU_valid_load_a5$_DFF_P_
            (rising edge-triggered flip-flop clocked by clk)
Endpoint: core.CPU_Xreg_value_a4[14][18]$_SDFFE_PP0P_
          (rising edge-triggered flip-flop clocked by clk)
Path Group: clk
Path Type: max

Fanout     Cap    Slew   Delay    Time   Description
-----------------------------------------------------------------------------
                  0.00    0.00    0.00   clock clk (rise edge)
                          0.00    0.00   clock network delay (ideal)
                  0.00    0.00    0.00 ^ core.CPU_valid_load_a5$_DFF_P_/CLK (sky130_fd_sc_hd__dfxtp_1)
     2    0.02    0.15    0.36    0.36 ^ core.CPU_valid_load_a5$_DFF_P_/Q (sky130_fd_sc_hd__dfxtp_1)
                                         core.CPU_valid_load_a5 (net)
                  0.15    0.00    0.36 ^ _05805_/D (sky130_fd_sc_hd__or4_4)
    48    0.47    1.32    1.04    1.41 ^ _05805_/X (sky130_fd_sc_hd__or4_4)
                                         _01035_ (net)
                  1.32    0.01    1.42 ^ _05806_/A (sky130_fd_sc_hd__clkinv_16)
    48    0.45    0.53    0.56    1.98 v _05806_/Y (sky130_fd_sc_hd__clkinv_16)
                                         _01036_ (net)
                  0.53    0.01    1.99 v _07859_/C (sky130_fd_sc_hd__nor3_1)
     1    0.01    0.27    0.35    2.35 ^ _07859_/Y (sky130_fd_sc_hd__nor3_1)
                                         _02490_ (net)
                  0.27    0.00    2.35 ^ _07860_/B1 (sky130_fd_sc_hd__a21oi_2)
     3    0.02    0.14    0.12    2.47 v _07860_/Y (sky130_fd_sc_hd__a21oi_2)
                                         _02491_ (net)
                  0.14    0.00    2.47 v _07956_/B (sky130_fd_sc_hd__nor3_4)
     4    0.08    0.77    0.67    3.14 ^ _07956_/Y (sky130_fd_sc_hd__nor3_4)
                                         _02586_ (net)
                  0.77    0.00    3.14 ^ _08969_/A (sky130_fd_sc_hd__nand2_8)
    49    0.27    0.43    0.48    3.62 v _08969_/Y (sky130_fd_sc_hd__nand2_8)
                                         _03467_ (net)
                  0.43    0.02    3.64 v _08993_/B (sky130_fd_sc_hd__nor2_2)
     5    0.03    0.32    0.40    4.04 ^ _08993_/Y (sky130_fd_sc_hd__nor2_2)
                                         _03483_ (net)
                  0.32    0.00    4.04 ^ _08994_/B1 (sky130_fd_sc_hd__o21ai_0)
     1    0.00    0.10    0.14    4.18 v _08994_/Y (sky130_fd_sc_hd__o21ai_0)
                                         _03484_ (net)
                  0.10    0.00    4.18 v _08997_/A1 (sky130_fd_sc_hd__a21oi_1)
     1    0.00    0.10    0.13    4.32 ^ _08997_/Y (sky130_fd_sc_hd__a21oi_1)
                                         _00681_ (net)
                  0.10    0.00    4.32 ^ core.CPU_Xreg_value_a4[14][18]$_SDFFE_PP0P_/D (sky130_fd_sc_hd__dfxtp_1)
                                  4.32   data arrival time

                  0.00    9.50    9.50   clock clk (rise edge)
                          0.00    9.50   clock network delay (ideal)
                          0.00    9.50   clock reconvergence pessimism
                                  9.50 ^ core.CPU_Xreg_value_a4[14][18]$_SDFFE_PP0P_/CLK (sky130_fd_sc_hd__dfxtp_1)
                         -0.07    9.43   library setup time
                                  9.43   data required time
-----------------------------------------------------------------------------
                                  9.43   data required time
                                 -4.32   data arrival time
-----------------------------------------------------------------------------
                                  5.11   slack (MET)



==========================================================================
detailed place report_check_types -max_slew -max_cap -max_fanout -violators
--------------------------------------------------------------------------

==========================================================================
detailed place max_slew_check_slack
--------------------------------------------------------------------------
0.1733454465866089

==========================================================================
detailed place max_slew_check_limit
--------------------------------------------------------------------------
1.5

==========================================================================
detailed place max_slew_check_slack_limit
--------------------------------------------------------------------------
0.1156

==========================================================================
detailed place max_fanout_check_slack
--------------------------------------------------------------------------
1.0000000150474662e+30

==========================================================================
detailed place max_fanout_check_limit
--------------------------------------------------------------------------
1.0000000150474662e+30

==========================================================================
detailed place max_capacitance_check_slack
--------------------------------------------------------------------------
0.01714012771844864

==========================================================================
detailed place max_capacitance_check_limit
--------------------------------------------------------------------------
0.021067000925540924

==========================================================================
detailed place max_capacitance_check_slack_limit
--------------------------------------------------------------------------
0.8136

==========================================================================
detailed place max_slew_violation_count
--------------------------------------------------------------------------
max slew violation count 0

==========================================================================
detailed place max_fanout_violation_count
--------------------------------------------------------------------------
max fanout violation count 0

==========================================================================
detailed place max_cap_violation_count
--------------------------------------------------------------------------
max cap violation count 0

==========================================================================
detailed place setup_violation_count
--------------------------------------------------------------------------
setup violation count 0

==========================================================================
detailed place hold_violation_count
--------------------------------------------------------------------------
hold violation count 0

==========================================================================
detailed place report_checks -path_delay max reg to reg
--------------------------------------------------------------------------
Startpoint: core.CPU_valid_load_a5$_DFF_P_
            (rising edge-triggered flip-flop clocked by clk)
Endpoint: core.CPU_Xreg_value_a4[14][18]$_SDFFE_PP0P_
          (rising edge-triggered flip-flop clocked by clk)
Path Group: clk
Path Type: max

  Delay    Time   Description
---------------------------------------------------------
   0.00    0.00   clock clk (rise edge)
   0.00    0.00   clock network delay (ideal)
   0.00    0.00 ^ core.CPU_valid_load_a5$_DFF_P_/CLK (sky130_fd_sc_hd__dfxtp_1)
   0.36    0.36 ^ core.CPU_valid_load_a5$_DFF_P_/Q (sky130_fd_sc_hd__dfxtp_1)
   1.04    1.41 ^ _05805_/X (sky130_fd_sc_hd__or4_4)
   0.58    1.98 v _05806_/Y (sky130_fd_sc_hd__clkinv_16)
   0.36    2.35 ^ _07859_/Y (sky130_fd_sc_hd__nor3_1)
   0.12    2.47 v _07860_/Y (sky130_fd_sc_hd__a21oi_2)
   0.67    3.14 ^ _07956_/Y (sky130_fd_sc_hd__nor3_4)
   0.48    3.62 v _08969_/Y (sky130_fd_sc_hd__nand2_8)
   0.42    4.04 ^ _08993_/Y (sky130_fd_sc_hd__nor2_2)
   0.15    4.18 v _08994_/Y (sky130_fd_sc_hd__o21ai_0)
   0.13    4.32 ^ _08997_/Y (sky130_fd_sc_hd__a21oi_1)
   0.00    4.32 ^ core.CPU_Xreg_value_a4[14][18]$_SDFFE_PP0P_/D (sky130_fd_sc_hd__dfxtp_1)
           4.32   data arrival time

   9.50    9.50   clock clk (rise edge)
   0.00    9.50   clock network delay (ideal)
   0.00    9.50   clock reconvergence pessimism
           9.50 ^ core.CPU_Xreg_value_a4[14][18]$_SDFFE_PP0P_/CLK (sky130_fd_sc_hd__dfxtp_1)
  -0.07    9.43   library setup time
           9.43   data required time
---------------------------------------------------------
           9.43   data required time
          -4.32   data arrival time
---------------------------------------------------------
           5.11   slack (MET)



==========================================================================
detailed place report_checks -path_delay min reg to reg
--------------------------------------------------------------------------
Startpoint: core.CPU_imm_a2[11]$_DFF_P_
            (rising edge-triggered flip-flop clocked by clk)
Endpoint: core.CPU_imm_a3[11]$_DFF_P_
          (rising edge-triggered flip-flop clocked by clk)
Path Group: clk
Path Type: min

  Delay    Time   Description
---------------------------------------------------------
   0.00    0.00   clock clk (rise edge)
   0.00    0.00   clock network delay (ideal)
   0.00    0.00 ^ core.CPU_imm_a2[11]$_DFF_P_/CLK (sky130_fd_sc_hd__dfxtp_1)
   0.28    0.28 ^ core.CPU_imm_a2[11]$_DFF_P_/Q (sky130_fd_sc_hd__dfxtp_1)
   0.00    0.28 ^ core.CPU_imm_a3[11]$_DFF_P_/D (sky130_fd_sc_hd__dfxtp_2)
           0.28   data arrival time

   0.00    0.00   clock clk (rise edge)
   0.00    0.00   clock network delay (ideal)
   0.00    0.00   clock reconvergence pessimism
           0.00 ^ core.CPU_imm_a3[11]$_DFF_P_/CLK (sky130_fd_sc_hd__dfxtp_2)
  -0.04   -0.04   library hold time
          -0.04   data required time
---------------------------------------------------------
          -0.04   data required time
          -0.28   data arrival time
---------------------------------------------------------
           0.31   slack (MET)



==========================================================================
detailed place critical path target clock latency max path
--------------------------------------------------------------------------
0

==========================================================================
detailed place critical path target clock latency min path
--------------------------------------------------------------------------
0

==========================================================================
detailed place critical path source clock latency min path
--------------------------------------------------------------------------
0

==========================================================================
detailed place critical path delay
--------------------------------------------------------------------------
4.3164

==========================================================================
detailed place critical path slack
--------------------------------------------------------------------------
5.1097

==========================================================================
detailed place slack div critical path delay
--------------------------------------------------------------------------
118.378742

==========================================================================
detailed place report_power
--------------------------------------------------------------------------
Group                  Internal  Switching    Leakage      Total
                          Power      Power      Power      Power (Watts)
----------------------------------------------------------------
Sequential             5.99e-03   9.64e-04   1.04e-08   6.96e-03  58.6%
Combinational          1.58e-03   3.35e-03   1.06e-08   4.92e-03  41.4%
Clock                  0.00e+00   0.00e+00   0.00e+00   0.00e+00   0.0%
Macro                  0.00e+00   0.00e+00   0.00e+00   0.00e+00   0.0%
Pad                    0.00e+00   0.00e+00   0.00e+00   0.00e+00   0.0%
----------------------------------------------------------------
Total                  7.57e-03   4.31e-03   2.10e-08   1.19e-02 100.0%
                          63.7%      36.3%       0.0%
```


## CTS

![image](https://github.com/user-attachments/assets/617f7ac5-4d5a-40bb-8278-8457aae93545)


```bash
make DESIGN_CONFIG=./designs/sky130hd/vsdbabysoc/config.mk cts
```

![image](https://github.com/user-attachments/assets/05219c63-5982-420c-923a-b2133273a99d)

![image](https://github.com/user-attachments/assets/919d59fe-d0ff-4652-92e3-5120e4dda6b1)

![image](https://github.com/user-attachments/assets/75f03593-4453-481a-aaa2-b4b15381be60)

![image](https://github.com/user-attachments/assets/7e498980-37cb-4b96-8de8-aeaef9fded10)

### Heatmaps:-

Placement density
![image](https://github.com/user-attachments/assets/74fa3141-7e1b-4cdc-a976-b1ede124ba14)

Power Density
![image](https://github.com/user-attachments/assets/5c80f708-5cdd-4169-8fcc-744a852f78d4)

Routing congesiton
![image](https://github.com/user-attachments/assets/201ae4be-b90d-4088-82c2-312fd985cec5)

Estimated Congestion
![image](https://github.com/user-attachments/assets/6bb3c1f7-fbaf-4609-9dd9-939943ce4fdf)

IR Drop
![image](https://github.com/user-attachments/assets/9f17ebc9-0aa0-4b57-a685-f9c62bc52310)


### CTS report

```bash


==========================================================================
cts final report_tns
--------------------------------------------------------------------------
tns 0.00

==========================================================================
cts final report_wns
--------------------------------------------------------------------------
wns 0.00

==========================================================================
cts final report_worst_slack
--------------------------------------------------------------------------
worst slack 5.07

==========================================================================
cts final report_clock_skew
--------------------------------------------------------------------------
Clock clk
   0.89 source latency core.CPU_dmem_rd_data_a5[11]$_DFF_P_/CLK ^
  -0.85 target latency core.CPU_Xreg_value_a4[14][11]$_SDFFE_PP0P_/CLK ^
   0.00 CRPR
--------------
   0.04 setup skew


==========================================================================
cts final report_checks -path_delay min
--------------------------------------------------------------------------
Startpoint: core.CPU_reset_a2$_DFF_P_
            (rising edge-triggered flip-flop clocked by clk)
Endpoint: core.CPU_reset_a3$_DFF_P_
          (rising edge-triggered flip-flop clocked by clk)
Path Group: clk
Path Type: min

Fanout     Cap    Slew   Delay    Time   Description
-----------------------------------------------------------------------------
                          0.00    0.00   clock clk (rise edge)
                          0.00    0.00   clock source latency
     1    0.31    0.00    0.00    0.00 ^ pll/CLK (avsdpll)
                                         CLK (net)
                  0.05    0.02    0.02 ^ clkbuf_0_CLK/A (sky130_fd_sc_hd__clkbuf_16)
    16    0.36    0.36    0.36    0.39 ^ clkbuf_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_0_CLK (net)
                  0.36    0.00    0.39 ^ clkbuf_4_8_0_CLK/A (sky130_fd_sc_hd__clkbuf_16)
    10    0.14    0.15    0.31    0.70 ^ clkbuf_4_8_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_4_8_0_CLK (net)
                  0.15    0.00    0.70 ^ clkbuf_leaf_18_CLK/A (sky130_fd_sc_hd__clkbuf_16)
     7    0.04    0.06    0.18    0.88 ^ clkbuf_leaf_18_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_leaf_18_CLK (net)
                  0.06    0.00    0.88 ^ core.CPU_reset_a2$_DFF_P_/CLK (sky130_fd_sc_hd__dfxtp_1)
     1    0.00    0.02    0.30    1.17 v core.CPU_reset_a2$_DFF_P_/Q (sky130_fd_sc_hd__dfxtp_1)
                                         core.CPU_reset_a2 (net)
                  0.02    0.00    1.17 v core.CPU_reset_a3$_DFF_P_/D (sky130_fd_sc_hd__dfxtp_4)
                                  1.17   data arrival time

                          0.00    0.00   clock clk (rise edge)
                          0.00    0.00   clock source latency
     1    0.31    0.00    0.00    0.00 ^ pll/CLK (avsdpll)
                                         CLK (net)
                  0.05    0.02    0.02 ^ clkbuf_0_CLK/A (sky130_fd_sc_hd__clkbuf_16)
    16    0.36    0.36    0.36    0.39 ^ clkbuf_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_0_CLK (net)
                  0.36    0.00    0.39 ^ clkbuf_4_8_0_CLK/A (sky130_fd_sc_hd__clkbuf_16)
    10    0.14    0.15    0.31    0.70 ^ clkbuf_4_8_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_4_8_0_CLK (net)
                  0.15    0.00    0.70 ^ clkbuf_leaf_17_CLK/A (sky130_fd_sc_hd__clkbuf_16)
     7    0.05    0.07    0.19    0.88 ^ clkbuf_leaf_17_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_leaf_17_CLK (net)
                  0.07    0.00    0.88 ^ core.CPU_reset_a3$_DFF_P_/CLK (sky130_fd_sc_hd__dfxtp_4)
                          0.00    0.88   clock reconvergence pessimism
                         -0.03    0.85   library hold time
                                  0.85   data required time
-----------------------------------------------------------------------------
                                  0.85   data required time
                                 -1.17   data arrival time
-----------------------------------------------------------------------------
                                  0.32   slack (MET)



==========================================================================
cts final report_checks -path_delay max
--------------------------------------------------------------------------
Startpoint: core.CPU_valid_load_a5$_DFF_P_
            (rising edge-triggered flip-flop clocked by clk)
Endpoint: core.CPU_Xreg_value_a4[14][18]$_SDFFE_PP0P_
          (rising edge-triggered flip-flop clocked by clk)
Path Group: clk
Path Type: max

Fanout     Cap    Slew   Delay    Time   Description
-----------------------------------------------------------------------------
                          0.00    0.00   clock clk (rise edge)
                          0.00    0.00   clock source latency
     1    0.31    0.00    0.00    0.00 ^ pll/CLK (avsdpll)
                                         CLK (net)
                  0.05    0.02    0.02 ^ clkbuf_0_CLK/A (sky130_fd_sc_hd__clkbuf_16)
    16    0.36    0.36    0.36    0.39 ^ clkbuf_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_0_CLK (net)
                  0.36    0.00    0.39 ^ clkbuf_4_8_0_CLK/A (sky130_fd_sc_hd__clkbuf_16)
    10    0.14    0.15    0.31    0.70 ^ clkbuf_4_8_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_4_8_0_CLK (net)
                  0.15    0.00    0.70 ^ clkbuf_leaf_13_CLK/A (sky130_fd_sc_hd__clkbuf_16)
    15    0.04    0.06    0.18    0.88 ^ clkbuf_leaf_13_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_leaf_13_CLK (net)
                  0.06    0.00    0.88 ^ core.CPU_valid_load_a5$_DFF_P_/CLK (sky130_fd_sc_hd__dfxtp_1)
     2    0.02    0.15    0.39    1.27 ^ core.CPU_valid_load_a5$_DFF_P_/Q (sky130_fd_sc_hd__dfxtp_1)
                                         core.CPU_valid_load_a5 (net)
                  0.15    0.00    1.27 ^ _05805_/D (sky130_fd_sc_hd__or4_4)
    48    0.47    1.33    1.04    2.31 ^ _05805_/X (sky130_fd_sc_hd__or4_4)
                                         _01035_ (net)
                  1.33    0.01    2.32 ^ _05806_/A (sky130_fd_sc_hd__clkinv_16)
    48    0.46    0.54    0.57    2.89 v _05806_/Y (sky130_fd_sc_hd__clkinv_16)
                                         _01036_ (net)
                  0.54    0.00    2.90 v _07859_/C (sky130_fd_sc_hd__nor3_1)
     1    0.01    0.27    0.35    3.25 ^ _07859_/Y (sky130_fd_sc_hd__nor3_1)
                                         _02490_ (net)
                  0.27    0.00    3.25 ^ _07860_/B1 (sky130_fd_sc_hd__a21oi_2)
     3    0.02    0.14    0.12    3.37 v _07860_/Y (sky130_fd_sc_hd__a21oi_2)
                                         _02491_ (net)
                  0.14    0.00    3.37 v _07956_/B (sky130_fd_sc_hd__nor3_4)
     4    0.08    0.77    0.67    4.05 ^ _07956_/Y (sky130_fd_sc_hd__nor3_4)
                                         _02586_ (net)
                  0.77    0.00    4.05 ^ _08969_/A (sky130_fd_sc_hd__nand2_8)
    49    0.27    0.43    0.48    4.52 v _08969_/Y (sky130_fd_sc_hd__nand2_8)
                                         _03467_ (net)
                  0.43    0.02    4.55 v _08993_/B (sky130_fd_sc_hd__nor2_2)
     5    0.03    0.33    0.40    4.95 ^ _08993_/Y (sky130_fd_sc_hd__nor2_2)
                                         _03483_ (net)
                  0.33    0.00    4.95 ^ _08994_/B1 (sky130_fd_sc_hd__o21ai_0)
     1    0.00    0.10    0.14    5.09 v _08994_/Y (sky130_fd_sc_hd__o21ai_0)
                                         _03484_ (net)
                  0.10    0.00    5.09 v _08997_/A1 (sky130_fd_sc_hd__a21oi_1)
     1    0.00    0.10    0.13    5.23 ^ _08997_/Y (sky130_fd_sc_hd__a21oi_1)
                                         _00681_ (net)
                  0.10    0.00    5.23 ^ core.CPU_Xreg_value_a4[14][18]$_SDFFE_PP0P_/D (sky130_fd_sc_hd__dfxtp_1)
                                  5.23   data arrival time

                          9.50    9.50   clock clk (rise edge)
                          0.00    9.50   clock source latency
     1    0.31    0.00    0.00    9.50 ^ pll/CLK (avsdpll)
                                         CLK (net)
                  0.05    0.02    9.52 ^ clkbuf_0_CLK/A (sky130_fd_sc_hd__clkbuf_16)
    16    0.36    0.36    0.36    9.89 ^ clkbuf_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_0_CLK (net)
                  0.36    0.00    9.89 ^ clkbuf_4_0_0_CLK/A (sky130_fd_sc_hd__clkbuf_16)
     7    0.12    0.14    0.29   10.18 ^ clkbuf_4_0_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_4_0_0_CLK (net)
                  0.14    0.00   10.18 ^ clkbuf_leaf_3_CLK/A (sky130_fd_sc_hd__clkbuf_16)
    13    0.04    0.06    0.18   10.36 ^ clkbuf_leaf_3_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_leaf_3_CLK (net)
                  0.06    0.00   10.36 ^ core.CPU_Xreg_value_a4[14][18]$_SDFFE_PP0P_/CLK (sky130_fd_sc_hd__dfxtp_1)
                          0.00   10.36   clock reconvergence pessimism
                         -0.06   10.29   library setup time
                                 10.29   data required time
-----------------------------------------------------------------------------
                                 10.29   data required time
                                 -5.23   data arrival time
-----------------------------------------------------------------------------
                                  5.07   slack (MET)



==========================================================================
cts final report_checks -unconstrained
--------------------------------------------------------------------------
Startpoint: core.CPU_valid_load_a5$_DFF_P_
            (rising edge-triggered flip-flop clocked by clk)
Endpoint: core.CPU_Xreg_value_a4[14][18]$_SDFFE_PP0P_
          (rising edge-triggered flip-flop clocked by clk)
Path Group: clk
Path Type: max

Fanout     Cap    Slew   Delay    Time   Description
-----------------------------------------------------------------------------
                          0.00    0.00   clock clk (rise edge)
                          0.00    0.00   clock source latency
     1    0.31    0.00    0.00    0.00 ^ pll/CLK (avsdpll)
                                         CLK (net)
                  0.05    0.02    0.02 ^ clkbuf_0_CLK/A (sky130_fd_sc_hd__clkbuf_16)
    16    0.36    0.36    0.36    0.39 ^ clkbuf_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_0_CLK (net)
                  0.36    0.00    0.39 ^ clkbuf_4_8_0_CLK/A (sky130_fd_sc_hd__clkbuf_16)
    10    0.14    0.15    0.31    0.70 ^ clkbuf_4_8_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_4_8_0_CLK (net)
                  0.15    0.00    0.70 ^ clkbuf_leaf_13_CLK/A (sky130_fd_sc_hd__clkbuf_16)
    15    0.04    0.06    0.18    0.88 ^ clkbuf_leaf_13_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_leaf_13_CLK (net)
                  0.06    0.00    0.88 ^ core.CPU_valid_load_a5$_DFF_P_/CLK (sky130_fd_sc_hd__dfxtp_1)
     2    0.02    0.15    0.39    1.27 ^ core.CPU_valid_load_a5$_DFF_P_/Q (sky130_fd_sc_hd__dfxtp_1)
                                         core.CPU_valid_load_a5 (net)
                  0.15    0.00    1.27 ^ _05805_/D (sky130_fd_sc_hd__or4_4)
    48    0.47    1.33    1.04    2.31 ^ _05805_/X (sky130_fd_sc_hd__or4_4)
                                         _01035_ (net)
                  1.33    0.01    2.32 ^ _05806_/A (sky130_fd_sc_hd__clkinv_16)
    48    0.46    0.54    0.57    2.89 v _05806_/Y (sky130_fd_sc_hd__clkinv_16)
                                         _01036_ (net)
                  0.54    0.00    2.90 v _07859_/C (sky130_fd_sc_hd__nor3_1)
     1    0.01    0.27    0.35    3.25 ^ _07859_/Y (sky130_fd_sc_hd__nor3_1)
                                         _02490_ (net)
                  0.27    0.00    3.25 ^ _07860_/B1 (sky130_fd_sc_hd__a21oi_2)
     3    0.02    0.14    0.12    3.37 v _07860_/Y (sky130_fd_sc_hd__a21oi_2)
                                         _02491_ (net)
                  0.14    0.00    3.37 v _07956_/B (sky130_fd_sc_hd__nor3_4)
     4    0.08    0.77    0.67    4.05 ^ _07956_/Y (sky130_fd_sc_hd__nor3_4)
                                         _02586_ (net)
                  0.77    0.00    4.05 ^ _08969_/A (sky130_fd_sc_hd__nand2_8)
    49    0.27    0.43    0.48    4.52 v _08969_/Y (sky130_fd_sc_hd__nand2_8)
                                         _03467_ (net)
                  0.43    0.02    4.55 v _08993_/B (sky130_fd_sc_hd__nor2_2)
     5    0.03    0.33    0.40    4.95 ^ _08993_/Y (sky130_fd_sc_hd__nor2_2)
                                         _03483_ (net)
                  0.33    0.00    4.95 ^ _08994_/B1 (sky130_fd_sc_hd__o21ai_0)
     1    0.00    0.10    0.14    5.09 v _08994_/Y (sky130_fd_sc_hd__o21ai_0)
                                         _03484_ (net)
                  0.10    0.00    5.09 v _08997_/A1 (sky130_fd_sc_hd__a21oi_1)
     1    0.00    0.10    0.13    5.23 ^ _08997_/Y (sky130_fd_sc_hd__a21oi_1)
                                         _00681_ (net)
                  0.10    0.00    5.23 ^ core.CPU_Xreg_value_a4[14][18]$_SDFFE_PP0P_/D (sky130_fd_sc_hd__dfxtp_1)
                                  5.23   data arrival time

                          9.50    9.50   clock clk (rise edge)
                          0.00    9.50   clock source latency
     1    0.31    0.00    0.00    9.50 ^ pll/CLK (avsdpll)
                                         CLK (net)
                  0.05    0.02    9.52 ^ clkbuf_0_CLK/A (sky130_fd_sc_hd__clkbuf_16)
    16    0.36    0.36    0.36    9.89 ^ clkbuf_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_0_CLK (net)
                  0.36    0.00    9.89 ^ clkbuf_4_0_0_CLK/A (sky130_fd_sc_hd__clkbuf_16)
     7    0.12    0.14    0.29   10.18 ^ clkbuf_4_0_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_4_0_0_CLK (net)
                  0.14    0.00   10.18 ^ clkbuf_leaf_3_CLK/A (sky130_fd_sc_hd__clkbuf_16)
    13    0.04    0.06    0.18   10.36 ^ clkbuf_leaf_3_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_leaf_3_CLK (net)
                  0.06    0.00   10.36 ^ core.CPU_Xreg_value_a4[14][18]$_SDFFE_PP0P_/CLK (sky130_fd_sc_hd__dfxtp_1)
                          0.00   10.36   clock reconvergence pessimism
                         -0.06   10.29   library setup time
                                 10.29   data required time
-----------------------------------------------------------------------------
                                 10.29   data required time
                                 -5.23   data arrival time
-----------------------------------------------------------------------------
                                  5.07   slack (MET)



==========================================================================
cts final report_check_types -max_slew -max_cap -max_fanout -violators
--------------------------------------------------------------------------

==========================================================================
cts final max_slew_check_slack
--------------------------------------------------------------------------
0.17144441604614258

==========================================================================
cts final max_slew_check_limit
--------------------------------------------------------------------------
1.5

==========================================================================
cts final max_slew_check_slack_limit
--------------------------------------------------------------------------
0.1143

==========================================================================
cts final max_fanout_check_slack
--------------------------------------------------------------------------
1.0000000150474662e+30

==========================================================================
cts final max_fanout_check_limit
--------------------------------------------------------------------------
1.0000000150474662e+30

==========================================================================
cts final max_capacitance_check_slack
--------------------------------------------------------------------------
0.01714012771844864

==========================================================================
cts final max_capacitance_check_limit
--------------------------------------------------------------------------
0.021067000925540924

==========================================================================
cts final max_capacitance_check_slack_limit
--------------------------------------------------------------------------
0.8136

==========================================================================
cts final max_slew_violation_count
--------------------------------------------------------------------------
max slew violation count 0

==========================================================================
cts final max_fanout_violation_count
--------------------------------------------------------------------------
max fanout violation count 0

==========================================================================
cts final max_cap_violation_count
--------------------------------------------------------------------------
max cap violation count 0

==========================================================================
cts final setup_violation_count
--------------------------------------------------------------------------
setup violation count 0

==========================================================================
cts final hold_violation_count
--------------------------------------------------------------------------
hold violation count 0

==========================================================================
cts final report_checks -path_delay max reg to reg
--------------------------------------------------------------------------
Startpoint: core.CPU_valid_load_a5$_DFF_P_
            (rising edge-triggered flip-flop clocked by clk)
Endpoint: core.CPU_Xreg_value_a4[14][18]$_SDFFE_PP0P_
          (rising edge-triggered flip-flop clocked by clk)
Path Group: clk
Path Type: max

  Delay    Time   Description
---------------------------------------------------------
   0.00    0.00   clock clk (rise edge)
   0.00    0.00   clock source latency
   0.00    0.00 ^ pll/CLK (avsdpll)
   0.39    0.39 ^ clkbuf_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
   0.31    0.70 ^ clkbuf_4_8_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
   0.18    0.88 ^ clkbuf_leaf_13_CLK/X (sky130_fd_sc_hd__clkbuf_16)
   0.00    0.88 ^ core.CPU_valid_load_a5$_DFF_P_/CLK (sky130_fd_sc_hd__dfxtp_1)
   0.39    1.27 ^ core.CPU_valid_load_a5$_DFF_P_/Q (sky130_fd_sc_hd__dfxtp_1)
   1.04    2.31 ^ _05805_/X (sky130_fd_sc_hd__or4_4)
   0.58    2.89 v _05806_/Y (sky130_fd_sc_hd__clkinv_16)
   0.36    3.25 ^ _07859_/Y (sky130_fd_sc_hd__nor3_1)
   0.12    3.37 v _07860_/Y (sky130_fd_sc_hd__a21oi_2)
   0.67    4.05 ^ _07956_/Y (sky130_fd_sc_hd__nor3_4)
   0.48    4.52 v _08969_/Y (sky130_fd_sc_hd__nand2_8)
   0.43    4.95 ^ _08993_/Y (sky130_fd_sc_hd__nor2_2)
   0.14    5.09 v _08994_/Y (sky130_fd_sc_hd__o21ai_0)
   0.13    5.23 ^ _08997_/Y (sky130_fd_sc_hd__a21oi_1)
   0.00    5.23 ^ core.CPU_Xreg_value_a4[14][18]$_SDFFE_PP0P_/D (sky130_fd_sc_hd__dfxtp_1)
           5.23   data arrival time

   9.50    9.50   clock clk (rise edge)
   0.00    9.50   clock source latency
   0.00    9.50 ^ pll/CLK (avsdpll)
   0.39    9.89 ^ clkbuf_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
   0.30   10.18 ^ clkbuf_4_0_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
   0.18   10.36 ^ clkbuf_leaf_3_CLK/X (sky130_fd_sc_hd__clkbuf_16)
   0.00   10.36 ^ core.CPU_Xreg_value_a4[14][18]$_SDFFE_PP0P_/CLK (sky130_fd_sc_hd__dfxtp_1)
   0.00   10.36   clock reconvergence pessimism
  -0.06   10.29   library setup time
          10.29   data required time
---------------------------------------------------------
          10.29   data required time
          -5.23   data arrival time
---------------------------------------------------------
           5.07   slack (MET)



==========================================================================
cts final report_checks -path_delay min reg to reg
--------------------------------------------------------------------------
Startpoint: core.CPU_reset_a2$_DFF_P_
            (rising edge-triggered flip-flop clocked by clk)
Endpoint: core.CPU_reset_a3$_DFF_P_
          (rising edge-triggered flip-flop clocked by clk)
Path Group: clk
Path Type: min

  Delay    Time   Description
---------------------------------------------------------
   0.00    0.00   clock clk (rise edge)
   0.00    0.00   clock source latency
   0.00    0.00 ^ pll/CLK (avsdpll)
   0.39    0.39 ^ clkbuf_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
   0.31    0.70 ^ clkbuf_4_8_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
   0.18    0.88 ^ clkbuf_leaf_18_CLK/X (sky130_fd_sc_hd__clkbuf_16)
   0.00    0.88 ^ core.CPU_reset_a2$_DFF_P_/CLK (sky130_fd_sc_hd__dfxtp_1)
   0.30    1.17 v core.CPU_reset_a2$_DFF_P_/Q (sky130_fd_sc_hd__dfxtp_1)
   0.00    1.17 v core.CPU_reset_a3$_DFF_P_/D (sky130_fd_sc_hd__dfxtp_4)
           1.17   data arrival time

   0.00    0.00   clock clk (rise edge)
   0.00    0.00   clock source latency
   0.00    0.00 ^ pll/CLK (avsdpll)
   0.39    0.39 ^ clkbuf_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
   0.31    0.70 ^ clkbuf_4_8_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
   0.19    0.88 ^ clkbuf_leaf_17_CLK/X (sky130_fd_sc_hd__clkbuf_16)
   0.00    0.88 ^ core.CPU_reset_a3$_DFF_P_/CLK (sky130_fd_sc_hd__dfxtp_4)
   0.00    0.88   clock reconvergence pessimism
  -0.03    0.85   library hold time
           0.85   data required time
---------------------------------------------------------
           0.85   data required time
          -1.17   data arrival time
---------------------------------------------------------
           0.32   slack (MET)



==========================================================================
cts final critical path target clock latency max path
--------------------------------------------------------------------------
0

==========================================================================
cts final critical path target clock latency min path
--------------------------------------------------------------------------
0

==========================================================================
cts final critical path source clock latency min path
--------------------------------------------------------------------------
0

==========================================================================
cts final critical path delay
--------------------------------------------------------------------------
5.2263

==========================================================================
cts final critical path slack
--------------------------------------------------------------------------
5.0678

==========================================================================
cts final slack div critical path delay
--------------------------------------------------------------------------
96.967262

==========================================================================
cts final report_power
--------------------------------------------------------------------------
Group                  Internal  Switching    Leakage      Total
                          Power      Power      Power      Power (Watts)
----------------------------------------------------------------
Sequential             5.87e-03   9.82e-04   1.04e-08   6.86e-03  39.8%
Combinational          1.58e-03   3.38e-03   1.06e-08   4.96e-03  28.8%
Clock                  2.99e-03   2.42e-03   2.21e-09   5.42e-03  31.4%
Macro                  0.00e+00   0.00e+00   0.00e+00   0.00e+00   0.0%
Pad                    0.00e+00   0.00e+00   0.00e+00   0.00e+00   0.0%
----------------------------------------------------------------
Total                  1.04e-02   6.78e-03   2.32e-08   1.72e-02 100.0%
                          60.6%      39.4%       0.0%

```

## Routing

```bash
make DESIGN_CONFIG=./designs/sky130hd/vsdbabysoc/config.mk route
```

![image](https://github.com/user-attachments/assets/546332ef-c385-4c45-a845-b334d97a2b48)

# ORFS for RVMYTH RISC-V :

The updated config file is as follows:-

```
export DESIGN_NICKNAME = rvmyth
export DESIGN_NAME = RV_CPU
export PLATFORM    = sky130hd

export VERILOG_FILES = $(DESIGN_HOME)/src/$(DESIGN_NICKNAME)/RV_CPU.v \
					   $(DESIGN_HOME)/src/$(DESIGN_NICKNAME)/include/clk_gate.v


export VERILOG_INCLUDE_DIRS = $(DESIGN_HOME)/src/$(DESIGN_NICKNAME)/include

export SDC_FILE = $(DESIGN_HOME)/$(PLATFORM)/$(DESIGN_NICKNAME)/constraint.sdc

export PDN_TCL = $(DESIGN_HOME)/$(PLATFORM)/$(DESIGN_NICKNAME)/pdn.tcl

export SYNTH_HIERARCHICAL = 1
export RTLMP_FLOW ?= 1

export PLACE_PINS_ARGS = -exclude left:0-150 -exclude left:300-500: -exclude right:* -exclude top:* -exclude bottom:*

export DIE_AREA   = 0 0 600 600
export CORE_AREA  = 20 20 590 590

export MACRO_PLACE_HALO = 50 50
export MACRO_PLACE_CHANNEL = 70 70
export TNS_END_PERCENT = 100

export REMOVE_ABC_BUFFERS = 1
```

The constraints file is as follows:-

```bash
set_units -time ns
set PERIOD 9.55
create_clock [get_ports {clk}] -name clk -period $PERIOD
set_clock_uncertainty [expr 0.05 * $PERIOD] -setup [get_clocks clk]
set_clock_uncertainty [expr 0.08 * $PERIOD] -hold [get_clocks clk]
set_clock_transition [expr 0.05 * $PERIOD] [get_clocks clk]

set_input_transition [expr $PERIOD * 0.08] [get_ports reset]

```

The Synthesis report is as follows:-

```bash
=== RV_CPU ===

   Number of wires:               7226
   Number of wire bits:           7235
   Number of public wires:        1401
   Number of public wire bits:    1410
   Number of ports:                  3
   Number of port bits:             12
   Number of memories:               0
   Number of memory bits:            0
   Number of processes:              0
   Number of cells:               7095
     sky130_fd_sc_hd__a2111o_1       1
     sky130_fd_sc_hd__a2111oi_0     15
     sky130_fd_sc_hd__a2111oi_1      7
     sky130_fd_sc_hd__a2111oi_2      9
     sky130_fd_sc_hd__a2111oi_4      2
     sky130_fd_sc_hd__a211o_1        4
     sky130_fd_sc_hd__a211oi_1      11
     sky130_fd_sc_hd__a211oi_2       2
     sky130_fd_sc_hd__a21bo_2        1
     sky130_fd_sc_hd__a21boi_0       7
     sky130_fd_sc_hd__a21boi_1       1
     sky130_fd_sc_hd__a21o_1        22
     sky130_fd_sc_hd__a21o_2         1
     sky130_fd_sc_hd__a21oi_1      905
     sky130_fd_sc_hd__a221o_1        2
     sky130_fd_sc_hd__a221oi_1      92
     sky130_fd_sc_hd__a22o_1        86
     sky130_fd_sc_hd__a22oi_1      504
     sky130_fd_sc_hd__a22oi_2        2
     sky130_fd_sc_hd__a2bb2oi_2      1
     sky130_fd_sc_hd__a311o_1        3
     sky130_fd_sc_hd__a311oi_1      19
     sky130_fd_sc_hd__a31o_2        18
     sky130_fd_sc_hd__a31oi_1       12
     sky130_fd_sc_hd__a41oi_1        4
     sky130_fd_sc_hd__a41oi_2        1
     sky130_fd_sc_hd__and2_0         1
     sky130_fd_sc_hd__and2_1        11
     sky130_fd_sc_hd__and3_1       109
     sky130_fd_sc_hd__and3b_1        1
     sky130_fd_sc_hd__and4_1         1
     sky130_fd_sc_hd__and4b_1        1
     sky130_fd_sc_hd__buf_1         44
     sky130_fd_sc_hd__buf_12         1
     sky130_fd_sc_hd__buf_2         19
     sky130_fd_sc_hd__buf_4          2
     sky130_fd_sc_hd__buf_6          1
     sky130_fd_sc_hd__clkbuf_1     609
     sky130_fd_sc_hd__conb_1         1
     sky130_fd_sc_hd__dfxtp_1     1274
     sky130_fd_sc_hd__fa_1           3
     sky130_fd_sc_hd__ha_1         135
     sky130_fd_sc_hd__inv_1        113
     sky130_fd_sc_hd__mux2_2         1
     sky130_fd_sc_hd__mux2i_1       54
     sky130_fd_sc_hd__nand2_1     1440
     sky130_fd_sc_hd__nand2b_1      31
     sky130_fd_sc_hd__nand3_1      290
     sky130_fd_sc_hd__nand3b_1      33
     sky130_fd_sc_hd__nand4_1      128
     sky130_fd_sc_hd__nand4b_1       1
     sky130_fd_sc_hd__nor2_1       230
     sky130_fd_sc_hd__nor2b_1       51
     sky130_fd_sc_hd__nor3_1        56
     sky130_fd_sc_hd__nor3_2         2
     sky130_fd_sc_hd__nor3b_1        3
     sky130_fd_sc_hd__nor4_1        28
     sky130_fd_sc_hd__nor4_2         1
     sky130_fd_sc_hd__o2111a_1       3
     sky130_fd_sc_hd__o2111ai_1      3
     sky130_fd_sc_hd__o211a_1        1
     sky130_fd_sc_hd__o211ai_1      38
     sky130_fd_sc_hd__o21a_1         8
     sky130_fd_sc_hd__o21ai_0      242
     sky130_fd_sc_hd__o21ai_1       12
     sky130_fd_sc_hd__o21ba_2        3
     sky130_fd_sc_hd__o21bai_1      24
     sky130_fd_sc_hd__o221ai_1      78
     sky130_fd_sc_hd__o221ai_4       1
     sky130_fd_sc_hd__o22a_1        34
     sky130_fd_sc_hd__o22ai_1       72
     sky130_fd_sc_hd__o311a_1        2
     sky130_fd_sc_hd__o311ai_0       3
     sky130_fd_sc_hd__o311ai_1       1
     sky130_fd_sc_hd__o31a_1         5
     sky130_fd_sc_hd__o31ai_1       56
     sky130_fd_sc_hd__o32a_1         2
     sky130_fd_sc_hd__o32ai_1        2
     sky130_fd_sc_hd__o41ai_1        3
     sky130_fd_sc_hd__or2_0          1
     sky130_fd_sc_hd__or2_2         11
     sky130_fd_sc_hd__or3_1         10
     sky130_fd_sc_hd__or3b_1         2
     sky130_fd_sc_hd__or3b_2         2
     sky130_fd_sc_hd__or4_1         11
     sky130_fd_sc_hd__or4b_1         1
     sky130_fd_sc_hd__xnor2_1       47
     sky130_fd_sc_hd__xnor2_2        1
     sky130_fd_sc_hd__xor2_1         9

   Chip area for module '\RV_CPU': 57322.476800
     of which used for sequential elements: 25504.460800 (44.49%)


```

## Clock Tree GUI

![image](https://github.com/user-attachments/assets/dd15a52f-a794-45d8-913e-af762c5a00c5)

## IR DROP

![image](https://github.com/user-attachments/assets/7900dab5-f817-4230-8c1b-779cd0ba39e5)

## Final Placement

![image](https://github.com/user-attachments/assets/7a7be6e2-715c-493a-a5ed-ce32fd4f3011)

## Final Routing GUI

![image](https://github.com/user-attachments/assets/535d575a-1ad0-490e-984d-90f72573ac1d)

![image](https://github.com/user-attachments/assets/8dbad7ad-211d-4577-b037-38f0a025ac89)

# QOR Results

![image](https://github.com/user-attachments/assets/5f6022f6-eaab-4752-b552-593a85c9ed1d)

## Final Timing Results


```bash
==========================================================================
cts final report_checks -path_delay min
--------------------------------------------------------------------------
Startpoint: CPU_reset_a3$_DFF_P_
            (rising edge-triggered flip-flop clocked by clk)
Endpoint: CPU_Xreg_value_a4[7][3]$_SDFFE_PP0P_
          (rising edge-triggered flip-flop clocked by clk)
Path Group: clk
Path Type: min

Fanout     Cap    Slew   Delay    Time   Description
-----------------------------------------------------------------------------
                          0.00    0.00   clock clk (rise edge)
                          0.00    0.00   clock source latency
     1    0.08    0.00    0.00    0.00 ^ clk (in)
                                         clk (net)
                  0.00    0.00    0.00 ^ clkbuf_0_clk/A (sky130_fd_sc_hd__clkbuf_16)
    16    0.37    0.37    0.35    0.35 ^ clkbuf_0_clk/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_0_clk (net)
                  0.37    0.00    0.36 ^ clkbuf_4_0_0_clk/A (sky130_fd_sc_hd__clkbuf_16)
     8    0.11    0.13    0.29    0.64 ^ clkbuf_4_0_0_clk/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_4_0_0_clk (net)
                  0.13    0.00    0.64 ^ clkbuf_leaf_121_clk/A (sky130_fd_sc_hd__clkbuf_16)
     8    0.04    0.06    0.17    0.81 ^ clkbuf_leaf_121_clk/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_leaf_121_clk (net)
                  0.06    0.00    0.81 ^ CPU_reset_a3$_DFF_P_/CLK (sky130_fd_sc_hd__dfxtp_4)
    44    0.25    0.30    0.56    1.38 v CPU_reset_a3$_DFF_P_/Q (sky130_fd_sc_hd__dfxtp_4)
                                         CPU_reset_a3 (net)
                  0.30    0.00    1.38 v _09858_/A (sky130_fd_sc_hd__nor2_1)
     1    0.00    0.07    0.17    1.55 ^ _09858_/Y (sky130_fd_sc_hd__nor2_1)
                                         _00953_ (net)
                  0.07    0.00    1.55 ^ CPU_Xreg_value_a4[7][3]$_SDFFE_PP0P_/D (sky130_fd_sc_hd__dfxtp_1)
                                  1.55   data arrival time

                          0.00    0.00   clock clk (rise edge)
                          0.00    0.00   clock source latency
     1    0.08    0.00    0.00    0.00 ^ clk (in)
                                         clk (net)
                  0.00    0.00    0.00 ^ clkbuf_0_clk/A (sky130_fd_sc_hd__clkbuf_16)
    16    0.37    0.37    0.35    0.35 ^ clkbuf_0_clk/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_0_clk (net)
                  0.37    0.00    0.36 ^ clkbuf_4_0_0_clk/A (sky130_fd_sc_hd__clkbuf_16)
     8    0.11    0.13    0.29    0.64 ^ clkbuf_4_0_0_clk/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_4_0_0_clk (net)
                  0.13    0.00    0.64 ^ clkbuf_leaf_1_clk/A (sky130_fd_sc_hd__clkbuf_16)
    13    0.04    0.06    0.17    0.82 ^ clkbuf_leaf_1_clk/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_leaf_1_clk (net)
                  0.06    0.00    0.82 ^ CPU_Xreg_value_a4[7][3]$_SDFFE_PP0P_/CLK (sky130_fd_sc_hd__dfxtp_1)
                          0.76    1.58   clock uncertainty
                          0.00    1.58   clock reconvergence pessimism
                         -0.03    1.55   library hold time
                                  1.55   data required time
-----------------------------------------------------------------------------
                                  1.55   data required time
                                 -1.55   data arrival time
-----------------------------------------------------------------------------
                                  0.00   slack (MET)

```

## ORFS flow to VSD BABY SOC:

We need to add the following files in the config.mk file

```bash

export DESIGN_NICKNAME = vsdbabysoc
export DESIGN_NAME = vsdbabysoc
export PLATFORM    = sky130hd

export ADDITIONAL_LIBS = $(DESIGN_HOME)/src/$(DESIGN_NICKNAME)/lib/avsddac.lib \
				         $(DESIGN_HOME)/src/$(DESIGN_NICKNAME)/lib/avsdpll.lib

export VERILOG_FILES = $(DESIGN_HOME)/src/$(DESIGN_NICKNAME)/vsdbabysoc.v \
					   $(DESIGN_HOME)/src/$(DESIGN_NICKNAME)/RV_CPU.v \
					   $(DESIGN_HOME)/src/$(DESIGN_NICKNAME)/include/clk_gate.v

export VERILOG_INCLUDE_DIRS = $(DESIGN_HOME)/src/$(DESIGN_NICKNAME)/include

export SDC_FILE      = $(DESIGN_HOME)/$(PLATFORM)/$(DESIGN_NICKNAME)/constraint.sdc

export ADDITIONAL_LEFS = $(DESIGN_HOME)/src/$(DESIGN_NICKNAME)/lef/avsddac.lef \
 						 $(DESIGN_HOME)/src/$(DESIGN_NICKNAME)/lef/avsdpll.lef


export ADDITIONAL_GDS = $(DESIGN_HOME)/src/$(DESIGN_NICKNAME)/gds/avsddac.gds \
						$(DESIGN_HOME)/src/$(DESIGN_NICKNAME)/gds/avsdpll.gds

export PDN_TCL = $(DESIGN_HOME)/$(PLATFORM)/$(DESIGN_NICKNAME)/pdn.tcl

export DIE_AREA   = 0 0 1600 1600
export CORE_AREA  = 20 20 1590 1590

export PLACE_PINS_ARGS = -exclude left:0-600 -exclude left:1000-1600: -exclude right:* -exclude top:* -exclude bottom:*
export MACRO_PLACEMENT = $(DESIGN_HOME)/$(PLATFORM)/$(DESIGN_NICKNAME)/macro_placement.cfg

export TNS_END_PERCENT = 100

export REMOVE_ABC_BUFFERS = 1

```

The constraints file is as follows:-

```bash

set_units -time ns
set PERIOD 9.50
create_clock [get_pins {pll/CLK}] -name clk -period $PERIOD
set_clock_uncertainty [expr 0.05 * $PERIOD] -setup [get_clocks clk]
set_clock_uncertainty [expr 0.08 * $PERIOD] -hold [get_clocks clk]
set_clock_transition [expr 0.05 * $PERIOD] [get_clocks clk]

set_input_transition [expr $PERIOD * 0.08] [get_ports ENb_CP]
set_input_transition [expr $PERIOD * 0.08] [get_ports ENb_VCO]
set_input_transition [expr $PERIOD * 0.08] [get_ports REF]
set_input_transition [expr $PERIOD * 0.08] [get_ports VCO_IN]
set_input_transition [expr $PERIOD * 0.08] [get_ports VREFH]
```

The synthesis report is as follows:-

```bash
=== vsdbabysoc ===

   Number of wires:               7221
   Number of wire bits:           7221
   Number of public wires:        1416
   Number of public wire bits:    1416
   Number of ports:                  7
   Number of port bits:              7
   Number of memories:               0
   Number of memory bits:            0
   Number of processes:              0
   Number of cells:               7077
     avsddac                         1
     avsdpll                         1
     sky130_fd_sc_hd__a2111oi_0     15
     sky130_fd_sc_hd__a2111oi_1      1
     sky130_fd_sc_hd__a2111oi_2      2
     sky130_fd_sc_hd__a211oi_1      20
     sky130_fd_sc_hd__a211oi_2       3
     sky130_fd_sc_hd__a21bo_2        1
     sky130_fd_sc_hd__a21boi_0       8
     sky130_fd_sc_hd__a21boi_2       1
     sky130_fd_sc_hd__a21o_1        30
     sky130_fd_sc_hd__a21oi_1      814
     sky130_fd_sc_hd__a221o_1        3
     sky130_fd_sc_hd__a221oi_1     101
     sky130_fd_sc_hd__a22o_1        95
     sky130_fd_sc_hd__a22oi_1      517
     sky130_fd_sc_hd__a311oi_1      41
     sky130_fd_sc_hd__a311oi_2       9
     sky130_fd_sc_hd__a31o_2         2
     sky130_fd_sc_hd__a31oi_1       18
     sky130_fd_sc_hd__a31oi_2        1
     sky130_fd_sc_hd__a32o_1         2
     sky130_fd_sc_hd__a41oi_1        2
     sky130_fd_sc_hd__and2_0         1
     sky130_fd_sc_hd__and2_1        12
     sky130_fd_sc_hd__and3_1        24
     sky130_fd_sc_hd__and3b_1        2
     sky130_fd_sc_hd__and4_1         2
     sky130_fd_sc_hd__buf_1         49
     sky130_fd_sc_hd__buf_2         10
     sky130_fd_sc_hd__buf_6          2
     sky130_fd_sc_hd__clkbuf_1     599
     sky130_fd_sc_hd__clkbuf_2       2
     sky130_fd_sc_hd__conb_1         1
     sky130_fd_sc_hd__dfxtp_1     1274
     sky130_fd_sc_hd__fa_1           3
     sky130_fd_sc_hd__ha_1         135
     sky130_fd_sc_hd__inv_1        110
     sky130_fd_sc_hd__mux2_2         2
     sky130_fd_sc_hd__mux2i_1       27
     sky130_fd_sc_hd__nand2_1     1407
     sky130_fd_sc_hd__nand2b_1      30
     sky130_fd_sc_hd__nand3_1      333
     sky130_fd_sc_hd__nand3b_1      38
     sky130_fd_sc_hd__nand4_1      120
     sky130_fd_sc_hd__nor2_1       319
     sky130_fd_sc_hd__nor2b_1       55
     sky130_fd_sc_hd__nor3_1        69
     sky130_fd_sc_hd__nor3b_1        7
     sky130_fd_sc_hd__nor4_1        34
     sky130_fd_sc_hd__nor4b_1        2
     sky130_fd_sc_hd__nor4bb_1       1
     sky130_fd_sc_hd__o2111a_1       2
     sky130_fd_sc_hd__o2111ai_1      3
     sky130_fd_sc_hd__o211a_1        3
     sky130_fd_sc_hd__o211ai_1      36
     sky130_fd_sc_hd__o211ai_2       1
     sky130_fd_sc_hd__o21a_1         5
     sky130_fd_sc_hd__o21ai_0      354
     sky130_fd_sc_hd__o21ai_1        9
     sky130_fd_sc_hd__o21ba_2        1
     sky130_fd_sc_hd__o21bai_1      25
     sky130_fd_sc_hd__o221a_2        1
     sky130_fd_sc_hd__o221ai_1      33
     sky130_fd_sc_hd__o22a_1        36
     sky130_fd_sc_hd__o22ai_1       73
     sky130_fd_sc_hd__o2bb2ai_1      1
     sky130_fd_sc_hd__o311a_1        2
     sky130_fd_sc_hd__o311ai_0       3
     sky130_fd_sc_hd__o311ai_1       3
     sky130_fd_sc_hd__o311ai_4       2
     sky130_fd_sc_hd__o31a_1         2
     sky130_fd_sc_hd__o31ai_1       34
     sky130_fd_sc_hd__o31ai_2        1
     sky130_fd_sc_hd__o32ai_1        1
     sky130_fd_sc_hd__or2_2         10
     sky130_fd_sc_hd__or3_1         20
     sky130_fd_sc_hd__or4_1         10
     sky130_fd_sc_hd__or4_4          2
     sky130_fd_sc_hd__xnor2_1       39
     sky130_fd_sc_hd__xor2_1         7



   Chip area for module '\vsdbabysoc': 56739.417600
     of which used for sequential elements: 25504.460800 (44.95%)
```

## Clock Tree

![image](https://github.com/user-attachments/assets/e53399cd-66ad-4768-8d39-8630bce686fa)

## IR Drop

![image](https://github.com/user-attachments/assets/39383a4e-8749-44d9-afe2-cb43e267e160)

## Final Placement

![image](https://github.com/user-attachments/assets/e674ca34-5624-44a7-aa81-276c11d09ce8)

## Final Routing

![image](https://github.com/user-attachments/assets/a88791e3-ce38-4d93-b5df-20a25cb65003)

## Final Timing Report

```bash

==========================================================================
cts final report_checks -path_delay min
--------------------------------------------------------------------------
Startpoint: core.CPU_Xreg_value_a4[9][22]$_SDFFE_PP0P_
            (rising edge-triggered flip-flop clocked by clk)
Endpoint: core.CPU_src1_value_a3[22]$_DFF_P_
          (rising edge-triggered flip-flop clocked by clk)
Path Group: clk
Path Type: min

Fanout     Cap    Slew   Delay    Time   Description
-----------------------------------------------------------------------------
                          0.00    0.00   clock clk (rise edge)
                          0.00    0.00   clock source latency
     1    0.30    0.00    0.00    0.00 ^ pll/CLK (avsdpll)
                                         CLK (net)
                  0.05    0.02    0.02 ^ clkbuf_0_CLK/A (sky130_fd_sc_hd__clkbuf_16)
    16    0.36    0.37    0.36    0.39 ^ clkbuf_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_0_CLK (net)
                  0.37    0.00    0.39 ^ clkbuf_4_8_0_CLK/A (sky130_fd_sc_hd__clkbuf_16)
     9    0.12    0.14    0.30    0.69 ^ clkbuf_4_8_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_4_8_0_CLK (net)
                  0.14    0.00    0.69 ^ clkbuf_leaf_105_CLK/A (sky130_fd_sc_hd__clkbuf_16)
    11    0.04    0.06    0.17    0.86 ^ clkbuf_leaf_105_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_leaf_105_CLK (net)
                  0.06    0.00    0.86 ^ core.CPU_Xreg_value_a4[9][22]$_SDFFE_PP0P_/CLK (sky130_fd_sc_hd__dfxtp_1)
     3    0.01    0.09    0.35    1.21 ^ core.CPU_Xreg_value_a4[9][22]$_SDFFE_PP0P_/Q (sky130_fd_sc_hd__dfxtp_1)
                                         core.CPU_Xreg_value_a4[9][22] (net)
                  0.09    0.00    1.21 ^ _10345_/B2 (sky130_fd_sc_hd__a22oi_1)
     1    0.00    0.05    0.07    1.28 v _10345_/Y (sky130_fd_sc_hd__a22oi_1)
                                         _04450_ (net)
                  0.05    0.00    1.28 v _10346_/C (sky130_fd_sc_hd__nand3_1)
     1    0.01    0.08    0.10    1.38 ^ _10346_/Y (sky130_fd_sc_hd__nand3_1)
                                         _04451_ (net)
                  0.08    0.00    1.38 ^ _10347_/B2 (sky130_fd_sc_hd__o22ai_1)
     1    0.01    0.08    0.10    1.47 v _10347_/Y (sky130_fd_sc_hd__o22ai_1)
                                         _04452_ (net)
                  0.08    0.00    1.47 v _10348_/A0 (sky130_fd_sc_hd__mux2i_1)
     1    0.00    0.10    0.12    1.60 ^ _10348_/Y (sky130_fd_sc_hd__mux2i_1)
                                         core.CPU_src1_value_a2[22] (net)
                  0.10    0.00    1.60 ^ core.CPU_src1_value_a3[22]$_DFF_P_/D (sky130_fd_sc_hd__dfxtp_1)
                                  1.60   data arrival time

                          0.00    0.00   clock clk (rise edge)
                          0.00    0.00   clock source latency
     1    0.30    0.00    0.00    0.00 ^ pll/CLK (avsdpll)
                                         CLK (net)
                  0.05    0.02    0.02 ^ clkbuf_0_CLK/A (sky130_fd_sc_hd__clkbuf_16)
    16    0.36    0.37    0.36    0.39 ^ clkbuf_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_0_CLK (net)
                  0.37    0.00    0.39 ^ clkbuf_4_9_0_CLK/A (sky130_fd_sc_hd__clkbuf_16)
     9    0.13    0.15    0.30    0.69 ^ clkbuf_4_9_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_4_9_0_CLK (net)
                  0.15    0.00    0.69 ^ clkbuf_leaf_83_CLK/A (sky130_fd_sc_hd__clkbuf_16)
    13    0.04    0.06    0.18    0.87 ^ clkbuf_leaf_83_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_leaf_83_CLK (net)
                  0.06    0.00    0.87 ^ core.CPU_src1_value_a3[22]$_DFF_P_/CLK (sky130_fd_sc_hd__dfxtp_1)
                          0.76    1.64   clock uncertainty
                          0.00    1.64   clock reconvergence pessimism
                         -0.04    1.60   library hold time
                                  1.60   data required time
-----------------------------------------------------------------------------
                                  1.60   data required time
                                 -1.60   data arrival time
-----------------------------------------------------------------------------
                                  0.00   slack (MET)


==========================================================================
cts final report_checks -path_delay max
--------------------------------------------------------------------------
Startpoint: core.CPU_valid_load_a5$_DFF_P_
            (rising edge-triggered flip-flop clocked by clk)
Endpoint: core.CPU_Xreg_value_a4[14][21]$_SDFFE_PP0P_
          (rising edge-triggered flip-flop clocked by clk)
Path Group: clk
Path Type: max

Fanout     Cap    Slew   Delay    Time   Description
-----------------------------------------------------------------------------
                          0.00    0.00   clock clk (rise edge)
                          0.00    0.00   clock source latency
     1    0.30    0.00    0.00    0.00 ^ pll/CLK (avsdpll)
                                         CLK (net)
                  0.05    0.02    0.02 ^ clkbuf_0_CLK/A (sky130_fd_sc_hd__clkbuf_16)
    16    0.36    0.37    0.36    0.39 ^ clkbuf_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_0_CLK (net)
                  0.37    0.00    0.39 ^ clkbuf_4_13_0_CLK/A (sky130_fd_sc_hd__clkbuf_16)
     8    0.12    0.13    0.29    0.68 ^ clkbuf_4_13_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_4_13_0_CLK (net)
                  0.13    0.00    0.68 ^ clkbuf_leaf_59_CLK/A (sky130_fd_sc_hd__clkbuf_16)
    13    0.04    0.06    0.17    0.86 ^ clkbuf_leaf_59_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_leaf_59_CLK (net)
                  0.06    0.00    0.86 ^ core.CPU_valid_load_a5$_DFF_P_/CLK (sky130_fd_sc_hd__dfxtp_1)
     2    0.02    0.17    0.40    1.26 ^ core.CPU_valid_load_a5$_DFF_P_/Q (sky130_fd_sc_hd__dfxtp_1)
                                         core.CPU_valid_load_a5 (net)
                  0.17    0.00    1.26 ^ _05805_/D (sky130_fd_sc_hd__or4_4)
    48    0.47    1.32    1.02    2.28 ^ _05805_/X (sky130_fd_sc_hd__or4_4)
                                         _01035_ (net)
                  1.33    0.07    2.35 ^ _05806_/A (sky130_fd_sc_hd__clkinv_16)
    48    0.45    0.54    0.56    2.91 v _05806_/Y (sky130_fd_sc_hd__clkinv_16)
                                         _01036_ (net)
                  0.54    0.04    2.95 v _07859_/C (sky130_fd_sc_hd__nor3_1)
     1    0.01    0.29    0.37    3.32 ^ _07859_/Y (sky130_fd_sc_hd__nor3_1)
                                         _02490_ (net)
                  0.29    0.00    3.32 ^ _07860_/B1 (sky130_fd_sc_hd__a21oi_2)
     3    0.02    0.14    0.12    3.44 v _07860_/Y (sky130_fd_sc_hd__a21oi_2)
                                         _02491_ (net)
                  0.14    0.00    3.44 v _07956_/B (sky130_fd_sc_hd__nor3_4)
     4    0.08    0.77    0.67    4.11 ^ _07956_/Y (sky130_fd_sc_hd__nor3_4)
                                         _02586_ (net)
                  0.77    0.00    4.11 ^ _08969_/A (sky130_fd_sc_hd__nand2_8)
    49    0.28    0.44    0.49    4.60 v _08969_/Y (sky130_fd_sc_hd__nand2_8)
                                         _03467_ (net)
                  0.44    0.00    4.60 v _09007_/A2 (sky130_fd_sc_hd__a22oi_1)
     1    0.00    0.20    0.32    4.92 ^ _09007_/Y (sky130_fd_sc_hd__a22oi_1)
                                         _03493_ (net)
                  0.20    0.00    4.92 ^ _09008_/B (sky130_fd_sc_hd__nor2_1)
     1    0.00    0.07    0.06    4.98 v _09008_/Y (sky130_fd_sc_hd__nor2_1)
                                         _00685_ (net)
                  0.07    0.00    4.98 v hold1586/A (sky130_fd_sc_hd__dlygate4sd3_1)
     1    0.00    0.05    0.56    5.54 v hold1586/X (sky130_fd_sc_hd__dlygate4sd3_1)
                                         net1700 (net)
                  0.05    0.00    5.54 v core.CPU_Xreg_value_a4[14][21]$_SDFFE_PP0P_/D (sky130_fd_sc_hd__dfxtp_1)
                                  5.54   data arrival time

                          9.55    9.55   clock clk (rise edge)
                          0.00    9.55   clock source latency
     1    0.30    0.00    0.00    9.55 ^ pll/CLK (avsdpll)
                                         CLK (net)
                  0.05    0.02    9.57 ^ clkbuf_0_CLK/A (sky130_fd_sc_hd__clkbuf_16)
    16    0.36    0.37    0.36    9.94 ^ clkbuf_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_0_CLK (net)
                  0.37    0.00    9.94 ^ clkbuf_4_12_0_CLK/A (sky130_fd_sc_hd__clkbuf_16)
     6    0.11    0.12    0.29   10.23 ^ clkbuf_4_12_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_4_12_0_CLK (net)
                  0.12    0.00   10.23 ^ clkbuf_leaf_58_CLK/A (sky130_fd_sc_hd__clkbuf_16)
     9    0.04    0.06    0.17   10.39 ^ clkbuf_leaf_58_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_leaf_58_CLK (net)
                  0.06    0.00   10.39 ^ core.CPU_Xreg_value_a4[14][21]$_SDFFE_PP0P_/CLK (sky130_fd_sc_hd__dfxtp_1)
                         -0.48    9.92   clock uncertainty
                          0.00    9.92   clock reconvergence pessimism
                         -0.11    9.80   library setup time
                                  9.80   data required time
-----------------------------------------------------------------------------
                                  9.80   data required time
                                 -5.54   data arrival time
-----------------------------------------------------------------------------
                                  4.26   slack (MET)
```


Heatmap for VSDBabysoc and RISC-V core

![image](https://github.com/user-attachments/assets/aeb3531a-b3e2-436f-93b3-c38d78aa8bc5)

![image](https://github.com/user-attachments/assets/c4398ace-c42d-47b4-bdfb-7ddc9ce0769d)

