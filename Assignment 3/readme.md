# Assignment 3
### Task :- 
To find the output of the C program on the RISC V Compiler using the Spike command and debug the code
### Tools used
- **Software Tools:**
  - GCC (GNU Compiler Collection)
  - RISC-V GNU Compiler Toolchain
  - Spike RISC-V Simulator
  - Ubuntu OS
### In assignment 1 we have compiled and found the output of the c code using the GCC compiler and have found the sum of the n numbers. In assignment 2 we have looked at the assembly code for the same using the objdump command on the RISC V compiler. In assignment 3 we are going to have find the result of the n numbers on the RISCV compiler using the SPIKE command

## Code for compiling the objdump file
```bash
spike pk sum1ton.o
```
### The compiled code using SPIKE command
![The compiled code on gcc compiler](https://github.com/user-attachments/assets/d6f0c595-eb7e-4f02-b1a1-75c55a81f275)

### The assembly code for reference
![The assembly code for the above c code](https://github.com/user-attachments/assets/0cfcd558-5c24-442e-9e62-6980597b05ad)


## Code for debugging the assembly code obtained in assignment 2
```bash
spike -d pk sum1ton.o
```
### From the assembly code we can see that the first address is at 10184. In order to debug the code we need the program counter to point at this address location. Therefore we use the following command to place the program counter on the the location 10184.

```bash
until pc 0 10184
```

### The first instruction involves the stack pointer. Therefore in order to check the initial and final contents of the stack pointer we use the follwoing code

```bash
reg 0 sp
```
### The following are the initial contents of the stack pointer

![stack pointer contents](https://github.com/user-attachments/assets/15734fb6-4390-4a8a-8c46-3d208c517225)
### In the assembly code we can see that the value of the stack pointer is being reduced by 10 in hexadecimal we is equivalent to being reduced by 16 in decimal notation
### After running the first line of the code the contents of the stack pointer get modified and we get the follwoing result

![modified sp](https://github.com/user-attachments/assets/03f6cb0c-2d06-42e1-a38c-36c63a921e6b)

### Similarly we can do the same for all the other instructions in the code and find out the contents in the respective addressing locations and their updated values once we execute the lines in the debugger.





