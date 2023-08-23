## Day 1


## Labwork for RISC-V software toolchain 

</details>	
	
<details>
 <summary> Program to Compute Sum from 1 to N </summary>
We have to write a C program using the commands below:

```bash
gedit sum1ton.c
```
![Screenshot from 2023-08-21 01-18-10](https://github.com/malobimukherjee/RISCV/assets/141206513/774dd6c6-ad37-4a75-a9c1-943b5aba7a5b)

And compile it by:

```bash
gcc sum1ton.c
./a.out
```
![Screenshot from 2023-08-21 01-21-50](https://github.com/malobimukherjee/RISCV/assets/141206513/9f22e0d6-a3cf-4cde-a06b-289bbb7d83c3)

</details>


 <details>
 <summary> RISCV GCC compile and Disassemble </summary>
 
 I used the following commands to run the code using riscv gcc compiler:
 
 ```bash
 cat sum1ton.c
riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c
```
![Screenshot from 2023-08-21 01-28-52](https://github.com/malobimukherjee/RISCV/assets/141206513/72ece38d-dde4-4967-806f-7596e3dc1c87)

It will generate a file like sum1ton.o

![Screenshot from 2023-08-21 01-32-31](https://github.com/malobimukherjee/RISCV/assets/141206513/2b58c15d-bc82-4f94-88f7-35f41f87736b)

To view the assembly code, I used the command:

```bash
riscv64-unknown-elf-objdump -d sum1ton.o
```

![Screenshot from 2023-08-21 01-38-02](https://github.com/malobimukherjee/RISCV/assets/141206513/81185092-8777-4fcd-be65-4fe0b54e2a45)

![Screenshot from 2023-08-21 01-41-08](https://github.com/malobimukherjee/RISCV/assets/141206513/1d49dfb0-2df4-44b8-8463-83f1ec17451e)

To view the main section, I typed:

```bash
/main
```
![Screenshot from 2023-08-21 01-43-39](https://github.com/malobimukherjee/RISCV/assets/141206513/2b9002a3-0378-47e4-b50e-1ed4bfa1608e)

Tried running the same command using -Ofast:

```bash
riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c
riscv64-unknown-elf-objdump -d sum1ton.o | less
```
![Screenshot from 2023-08-21 01-54-15](https://github.com/malobimukherjee/RISCV/assets/141206513/0565cdbd-6d12-432e-8d5f-e4e46891835f)

</details>


 <details>
 <summary> Spike Simulation And Debug </summary>

I used the command below to execute with the help of riscv compiler:

```bash
spike pk sum1ton.o
```
![Screenshot from 2023-08-21 02-02-01](https://github.com/malobimukherjee/RISCV/assets/141206513/113a3db6-d880-4d3d-bef3-4fc1287ab10b)

```bash
spike -d pk sum1ton.o
```
![Screenshot from 2023-08-21 02-18-11](https://github.com/malobimukherjee/RISCV/assets/141206513/98e60b94-2e0a-482c-81b0-a0b6fbab2554)

![Screenshot from 2023-08-21 02-21-33](https://github.com/malobimukherjee/RISCV/assets/141206513/aa91dabf-4a50-4cf7-ba7c-05a1031bd1c0)

</details>

## Integer Number Representation

<details>

<summary>Lab for Signed and Unsigned Numbers</summary>

I wrote a code for unsigned number:


![Screenshot from 2023-08-21 03-06-35](https://github.com/malobimukherjee/RISCV/assets/141206513/e4eaf0c4-ad70-4697-b82c-19729635f773)

And then executed the code using the command below:

```bash
riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o signedunsigned.o signedunsigned.c
spike pk signedunsigned.o
```

![Screenshot from 2023-08-21 03-08-45](https://github.com/malobimukherjee/RISCV/assets/141206513/4cf65509-c6c7-4cdc-ad25-efa7730c24db)

To check whether it shows signed number:

![Screenshot from 2023-08-21 03-17-53](https://github.com/malobimukherjee/RISCV/assets/141206513/e1aa7f0e-bda6-41f9-b029-003569b0cac0)

![Screenshot from 2023-08-21 03-19-36](https://github.com/malobimukherjee/RISCV/assets/141206513/21357e0d-4c45-4c8c-9aa1-2e7e39484313)

Modified the code for signed number:

![Screenshot from 2023-08-21 03-23-00](https://github.com/malobimukherjee/RISCV/assets/141206513/9862c085-4283-4fa3-b07b-d2081b2bcd75)


![Screenshot from 2023-08-21 03-23-34](https://github.com/malobimukherjee/RISCV/assets/141206513/d69da97e-877b-4303-b70f-afb4b4d29164)


</details>

## Day 2


## Introduction to ABI and Basic Verification Flow

<details>	

<summary> Simulate C program with ASM Function call </summary>

We have to write a C program using main function and use extern to call the ASM function:

```bash
gedit 1to9_custom.c
```

![Screenshot from 2023-08-22 23-11-04](https://github.com/malobimukherjee/RISCV/assets/141206513/4b90492b-7c2e-4446-bb6b-c6f5b36c7547)

Assembly language code:

```bash
gedit Load.S
```

![Screenshot from 2023-08-22 23-10-34](https://github.com/malobimukherjee/RISCV/assets/141206513/6282de5d-d28f-441e-a66e-43b1edc99993)


I used the riscv64 compiler and the spike simulator to see the ASM code:


```bash
riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o 1to9_custom.o 1to9_custom.c load.S
spike pk 1to9_custom.o
riscv64-unknown-elf-objdump -d 1to9_custom.o | less
```

![Screenshot from 2023-08-22 23-34-19](https://github.com/malobimukherjee/RISCV/assets/141206513/06c3bb17-7081-404e-ae55-57ae39298292)


![Screenshot from 2023-08-22 23-36-48](https://github.com/malobimukherjee/RISCV/assets/141206513/f09a9dfd-c6c8-4bd8-8b6f-2d63747141bb)


![Screenshot from 2023-08-22 23-38-55](https://github.com/malobimukherjee/RISCV/assets/141206513/57f86347-f4c2-409f-8b1c-cabdaae6d0b0)

</details>


<details>
	
<summary> Lab to run C program on RISCV CPU </summary>


I used the below commands:

```bash
cd riscv_workshop_collaterals
cd labs
ls -ltr
gedit 1to9_custom.c
chmod 777 rv32im.sh
 ./rv32im.sh
```
![Screenshot from 2023-08-22 23-54-51](https://github.com/malobimukherjee/RISCV/assets/141206513/e36ae58a-4ff7-416a-920d-aac4b7b82560)

</details>

## Day 3


## Digital Logic with TL-Verilog and Makerchip

<details>

<summary> Basic MUX implementation and Introduction to Makerchip </summary>

Website Link: https://www.makerchip.com/sandbox/#

I chose from the example code- FPGA Multiplier Code:

![Screenshot from 2023-08-23 04-26-40](https://github.com/malobimukherjee/RISCV/assets/141206513/6c6b6ecd-c90b-4053-851d-ded63d0c5ce3)


</details>
<details>


<summary>Lab for Combinational Logic</summary>

![Screenshot from 2023-08-23 04-48-20](https://github.com/malobimukherjee/RISCV/assets/141206513/ee18bcc7-1347-4641-83f5-c2124185abaa)

![Screenshot from 2023-08-23 04-50-06](https://github.com/malobimukherjee/RISCV/assets/141206513/e3c02ce4-a089-40ad-a7bf-2fa2ad390af6)

Combinational Calculator:

![Screenshot from 2023-08-23 05-16-04](https://github.com/malobimukherjee/RISCV/assets/141206513/6be7cc17-daae-4b87-b871-ab198b40c0b8)



</details>
<details>

<summary> Sequential Logic - Fibonacci Series </summary>

![Screenshot from 2023-08-23 05-31-06](https://github.com/malobimukherjee/RISCV/assets/141206513/12fc6055-a6cd-489f-b25c-9f33f4525f32)

</details>
<details>
<summary> Pipelined Logic </summary>


![Pythagorean_example_validity_check2](https://github.com/malobimukherjee/RISCV/assets/141206513/fa30c7cf-ad17-48e1-a82b-6ebcd26a4673)

## Lab on 2-Cycle calculator


![Screenshot from 2023-08-23 06-14-18](https://github.com/malobimukherjee/RISCV/assets/141206513/b8ccb1bc-2ed9-429a-a904-9f22a9e18381)

</details>
