# ASIC Design Lab report assignment 2

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

## Screenshots of the compiled result ##

![riscv gcc 01](https://github.com/user-attachments/assets/8d413890-5c3a-4883-a5d5-2a61c52349b4)

![riscv gcc ofast](https://github.com/user-attachments/assets/2c7477dc-4667-434a-9ef0-8624b6362f36)

### Step 2:- Get the assembly language code for the given c file

### Once we get the assembly language code we then verify the number of addresses in the code by subtracting the address next to the last line of the code with the first address and dividing the same by 4 since 4 bytes of data is used by each address line

![assembly code riscv gcc 01](https://github.com/user-attachments/assets/174a462f-eabc-4b51-abc1-e898e7c0a3ae)

![assembly code riscv gcc ofast](https://github.com/user-attachments/assets/9e6b5fe8-f404-4e4f-a537-656358699061)

