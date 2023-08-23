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

## Validity

<details>
<summary> Lab to Compute Total Distance </summary>

![Screenshot from 2023-08-23 11-00-24](https://github.com/malobimukherjee/RISCV/assets/141206513/44eae83f-d441-44fb-a8c1-fed633d22337)
 
</details>

<details>

<summary> Lab on 2-Cycle Calculator with Validity </summary>

![Screenshot from 2023-08-23 11-10-01](https://github.com/malobimukherjee/RISCV/assets/141206513/6de73103-95cc-4ca3-a438-661d2d83cb09)


</details>
<details>

<summary> Calculator with Single-Value Memory </summary>

![Screenshot from 2023-08-23 11-10-01](https://github.com/malobimukherjee/RISCV/assets/141206513/07001d95-4554-446a-89fd-25136a7aa5f7)

</details>

## Hierarchy

<details>

 <summary> Pythagorean Theorem using Behavioural Hierarchy</summary>
 
![Screenshot from 2023-08-23 11-19-20](https://github.com/malobimukherjee/RISCV/assets/141206513/12468bf9-af6e-439c-9786-d73b14043327)

 
</details>

## Day 4

<details>

<summary> Lab: Next PC </summary>
 
![Screenshot from 2023-08-23 11-29-11](https://github.com/malobimukherjee/RISCV/assets/141206513/30f3982a-9999-4069-8020-ba5d5faa2ce1)

 
</details>

<details>

<summary> Instruction Fetch Logic </summary>

![Screenshot from 2023-08-23 11-38-14](https://github.com/malobimukherjee/RISCV/assets/141206513/c9119092-dd1d-49d5-9abf-16e3dcfb16e7)

</details>

<details>

<summary> Instruction Decode </summary>

![Screenshot from 2023-08-23 11-34-20](https://github.com/malobimukherjee/RISCV/assets/141206513/3ed167b2-7ea1-4171-b33d-74b429cee890)

 
</details>

<details>

 <summary> Register File Read </summary>
 
![Screenshot from 2023-08-23 11-42-07](https://github.com/malobimukherjee/RISCV/assets/141206513/d755cd04-aa81-4dd0-80d7-8e4e178ad2d6)

 
</details>

<details>

 <summary> ALU </summary>

 ![Screenshot from 2023-08-23 11-46-19](https://github.com/malobimukherjee/RISCV/assets/141206513/9cf9cbc0-7009-4558-8b68-ff5595097ab5)


</details>

<details>

 <summary> Register File Write </summary>

![Screenshot from 2023-08-23 11-49-06](https://github.com/malobimukherjee/RISCV/assets/141206513/de6168ae-35c8-41c0-89fd-e11bf3d8fb2b)

</details>
<details>

 <summary>Branch Instruction</summary>

 ![Screenshot from 2023-08-23 11-52-29](https://github.com/malobimukherjee/RISCV/assets/141206513/60ac1095-9deb-44ea-a30d-ab53f3144a17)

</details>

<details>

 <summary> Final Output: RISCV Core </summary>

![Screenshot from 2023-08-23 11-56-14](https://github.com/malobimukherjee/RISCV/assets/141206513/ab7436dc-668c-4a88-bde3-b98201f68370)

 
</details>

## Day 5

<details> 

<summary> RISC-V CPU Core Final Code </summary>

```bash
\m4_TLV_version 1d: tl-x.org
\SV
   //  This code can be found in: https://github.com/stevehoover/RISC-V_MYTH_Workshop
   
   m4_include_lib(['https://raw.githubusercontent.com/stevehoover/RISC-V_MYTH_Workshop/c1719d5b338896577b79ee76c2f443ca2a76e14f/tlv_lib/risc-v_shell_lib.tlv'])

\SV
   m4_makerchip_module   // (Expanded in Nav-TLV pane.)
\TLV

   // /====================\
   // | Sum 1 to 9 Program |
   // \====================/
   //
   // Program for MYTH Workshop to test RV32I
   // Add 1,2,3,...,9 (in that order).
   //
   // Regs:
   //  r10 (a0): In: 0, Out: final sum
   //  r12 (a2): 10
   //  r13 (a3): 1..10
   //  r14 (a4): Sum
   // 
   // External to function:
   m4_asm(ADD, r10, r0, r0)             // Initialize r10 (a0) to 0.
   // Function:
   m4_asm(ADD, r14, r10, r0)            // Initialize sum register a4 with 0x0
   m4_asm(ADDI, r12, r10, 1010)         // Store count of 10 in register a2.
   m4_asm(ADD, r13, r10, r0)            // Initialize intermediate sum register a3 with 0
   // Loop:
   m4_asm(ADD, r14, r13, r14)           // Incremental addition
   m4_asm(ADDI, r13, r13, 1)            // Increment intermediate register by 1
   m4_asm(BLT, r13, r12, 1111111111000) // If a3 is less than a2, branch to label named <loop>
   m4_asm(ADD, r10, r14, r0)            // Store final result to register a0 so that it can be read by main program
   m4_asm(SW, r0, r10, 10000)           // Store the final result value to byte address 16
   m4_asm(LW, r17, r0, 10000)           // Load the final result value from adress 16 to x17
   
   // Optional:
   // m4_asm(JAL, r7, 00000000000000000000) // Done. Jump to itself (infinite loop). (Up to 20-bit signed immediate plus implicit 0 bit (unlike JALR) provides byte address; last immediate bit should also be 0)
   m4_define_hier(['M4_IMEM'], M4_NUM_INSTRS)
   
   |cpu
      @0
         $reset = *reset;
         
         //NEXT PC LOGIC       
         
         $pc[31:0] = >>1$reset ? 32'b0 :
                     >>3$valid_taken_branch ? >>3$br_target_pc :
                     >>3$valid_load ? >>3$inc_pc :
                     >>3$valid_jump && >>3$is_jal ? >>3$br_target_pc :
                     >>3$valid_jump && >>3$is_jalr ? >>3$jalr_target_pc :
                     >>1$inc_pc ;
      @1   
         $inc_pc[31:0] = $pc + 32'd4;
         
         
      @3
         //CYCLE VALID INSTRUCTIONS
         $valid = !(>>1$valid_taken_branch || >>2$valid_taken_branch || 
                    >>1$valid_load || >>2$valid_load ||  
                    >>1$valid_jump || >>2$valid_jump) ;
         
         $valid_load = $valid && $is_load ;
         
         $valid_jump = $is_jump && $valid ;
         
         
         
         //INSTRUCTION FETCH LOGIC
      @1 
         $imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         $imem_rd_en = !$reset;
         $instr[31:0] = $imem_rd_data[31:0];
         
         
         //INSTRUCTION TYPES DECODE   
      @1
         $is_u_instr = $instr[6:2] ==? 5'b0x101;
         
         $is_s_instr = $instr[6:2] ==? 5'b0100x;
         
         $is_r_instr = $instr[6:2] ==? 5'b01011 ||
                       $instr[6:2] ==? 5'b011x0 ||
                       $instr[6:2] ==? 5'b10100;
         
         $is_j_instr = $instr[6:2] ==? 5'b11011;
         
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                       $instr[6:2] ==? 5'b001x0 ||
                       $instr[6:2] ==? 5'b11001;
         
         $is_b_instr = $instr[6:2] ==? 5'b11000;
         
         
         //INSTRUCTION IMMEDIATE DECODE
         
         $imm[31:0] = $is_i_instr ? {{21{$instr[31]}}, $instr[30:20]} :
                      $is_s_instr ? {{21{$instr[31]}}, $instr[30:25], $instr[11:7]} :
                      $is_b_instr ? {{20{$instr[31]}}, $instr[7], $instr[30:25], $instr[11:8], 1'b0} :
                      $is_u_instr ? {$instr[31:12], 12'b0} :
                      $is_j_instr ? {{12{$instr[31]}}, $instr[19:12], $instr[20], $instr[30:21], 1'b0} :
                                    32'b0;
         `BOGUS_USE($imm)
         
         $opcode[6:0] = $instr[6:0];
         
         
         //INSTRUCTION FIELD DECODE
         
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
            
         `BOGUS_USE($rd)
         
      @2
         //INSTRUCTION DECODE
         $dec_bits[10:0] = {$funct7[5], $funct3, $opcode};
         $is_beq = $dec_bits ==? 11'bx_000_1100011;
         $is_bne = $dec_bits ==? 11'bx_001_1100011;
         $is_blt = $dec_bits ==? 11'bx_100_1100011;
         $is_bge = $dec_bits ==? 11'bx_101_1100011;
         $is_bltu = $dec_bits ==? 11'bx_110_1100011;
         $is_bgeu = $dec_bits ==? 11'bx_111_1100011;
         $is_addi = $dec_bits ==? 11'bx_000_0010011;
         $is_add = $dec_bits ==? 11'b0_000_0110011;
         
         $is_load = $opcode == 7'b0000011;
         
         $is_xori = $dec_bits ==? 11'bx_100_0010011;
         $is_xor = $dec_bits ==? 11'b0_100_0110011;
         $is_sw = $dec_bits ==? 11'bx_010_0100011;
         $is_sub = $dec_bits ==? 11'b1_000_0110011;
         $is_srli = $dec_bits ==? 11'b0_101_0010011;
         $is_srl = $dec_bits ==? 11'b0_101_0110011;
         $is_srai = $dec_bits ==? 11'b1_101_0010011;
         $is_sra = $dec_bits ==? 11'b1_101_0110011;
         $is_sltu = $dec_bits ==? 11'b0_011_0110011;
         $is_sltiu = $dec_bits ==? 11'bx_011_0010011;
         $is_slti = $dec_bits ==? 11'bx_010_0010011;
         $is_slt = $dec_bits ==? 11'b0_010_0110011;
         $is_slli = $dec_bits ==? 11'b0_001_0010011;
         $is_sll = $dec_bits ==? 11'b0_001_0110011;
         $is_sh = $dec_bits ==? 11'bx_001_0100011;
         $is_sb = $dec_bits ==? 11'bx_000_0100011;
         $is_ori = $dec_bits ==? 11'bx_110_0010011;
         $is_or = $dec_bits ==? 11'b0_110_0110011;
         $is_lui = $dec_bits ==? 11'bx_xxx_0110111;
         $is_jalr = $dec_bits ==? 11'bx_000_1100111;
         $is_jal = $dec_bits ==? 11'bx_xxx_1101111;
         $is_auipc = $dec_bits ==? 11'bx_xxx_0010111;
         $is_andi = $dec_bits ==? 11'bx_111_0010011;
         $is_and = $dec_bits ==? 11'b0_111_0110011;
         
         $jalr_target_pc[31:0] = $src1_value +$imm ;
         
      @3
         $is_jump = $is_jal || $is_jalr ;
         
         `BOGUS_USE ($is_beq $is_bne $is_blt $is_bge $is_bltu $is_bgeu $is_addi $is_add)
         
         
      @2
         //REGISTER FILE READ
         
         $rf_rd_en1 = $rs1_valid;
         $rf_rd_index1[4:0] = $rs1;
         $rf_rd_en2 = $rs2_valid;
         $rf_rd_index2[4:0] = $rs2;
         
      @3
         //REGISTER FILE WRITE
         $rf_wr_en = ($rd_valid && $rd != 5'b0 && $valid) || >>2$valid_load;
         $rf_wr_index[4:0] = >>2$valid_load ? >>2$rd : $rd;
         $rf_wr_data[31:0] = >>2$valid_load ? >>2$ld_data : $result;
         
      @2   
         $src1_value[31:0] = (>>1$rf_wr_index == $rf_rd_index1) && >>1$rf_wr_en ? >>1$result :  
                             $rf_rd_data1;
         
         $src2_value[31:0] = (>>1$rf_wr_index == $rf_rd_index2) && >>1$rf_wr_en ? >>1$result :
                             $rf_rd_data2;
         
      @4
         //MINI 1-R/W MEMORY
         $dmem_wr_en = $is_s_instr && $valid ;
         $dmem_addr[3:0] = $result[5:2] ;
         $dmem_wr_data[31:0] = $src2_value ;
         $dmem_rd_en = $is_load ;
         
      @5
         //LOAD DATA
         $ld_data[31:0] = $dmem_rd_data ;
         
         
      @3   
         //ARITHMETIC AND LOGIC UNIT (ALU)
         
         $sltu_rslt[31:0] = $src1_value < $src2_value ;
         $sltiu_rslt[31:0]  = $src1_value < $imm ;
         
         $result[31:0] = $is_andi ? $src1_value & $imm :
                         $is_ori ? $src1_value | $imm :
                         $is_xori ? $src1_value ^ $imm :
                         ($is_addi || $is_load || $is_s_instr) ? $src1_value + $imm :
                         $is_slli ? $src1_value << $imm[5:0] :
                         $is_srli ? $src1_value >> $imm[5:0] :
                         $is_and ? $src1_value & $src2_value :
                         $is_or ? $src1_value | $src2_value :
                         $is_xor ? $src1_value ^ $src2_value :
                         $is_add ? $src1_value + $src2_value :
                         $is_sub ? $src1_value - $src2_value :
                         $is_sll ? $src1_value << $src2_value[4:0] :
                         $is_srl ? $src1_value >> $src2_value[4:0] :
                         $is_sltu ? $src1_value | $src2_value :
                         $is_sltiu ? $src1_value < $imm :
                         $is_lui ? {$imm[31:12], 12'b0} :
                         $is_auipc ? $pc + $imm :
                         $is_jal ? $pc + 4 :
                         $is_jalr ? $pc + 4 :
                         $is_srai ? {{32{$src1_value[31]}}, $src1_value} >> $imm[4:0] :
                         $is_slt ? ($src1_value[31] == $src2_value[31]) ? $sltu_rslt : {31'b0, $src1_value[31]} :
                         $is_slti ? ($src1_value[31] == $imm[31]) ? $sltiu_rslt : {31'b0, $src1_value[31]} :
                         $is_sra ? {{32{$src1_value[31]}}, $src1_value} > $src2_value[4:0] :
                         32'bx ;
         
         
         //BRANCH INSTRUCTIONS 1
         $taken_branch = $is_beq ? ($src1_value == $src2_value):
                         $is_bne ? ($src1_value != $src2_value):
                         $is_blt ? (($src1_value < $src2_value) ^ ($src1_value[31] != $src2_value[31])):
                         $is_bge ? (($src1_value >= $src2_value) ^ ($src1_value[31] != $src2_value[31])):
                         $is_bltu ? ($src1_value < $src2_value):
                         $is_bgeu ? ($src1_value >= $src2_value):
                                    1'b0;
         
         $valid_taken_branch = $valid && $taken_branch;
                  
      @2
         //BRANCH INSTRUCTIONS 2
         $br_target_pc[31:0] = $pc +$imm;
         
         
         //TESTBENCH
         *passed = |cpu/xreg[17]>>5$value == (1+2+3+4+5+6+7+8+9) ;
         
         
      // Note: Because of the magic we are using for visualisation, if visualisation is enabled below,
      //       be sure to avoid having unassigned signals (which you might be using for random inputs)
      //       other than those specifically expected in the labs. You'll get strange errors for these.
   
   // Assert these to end simulation (before Makerchip cycle limit).
   *passed = *cyc_cnt > 40;
   *failed = 1'b0;
   
   // Macro instantiations for:
   //  o instruction memory
   //  o register file
   //  o data memory
   //  o CPU visualization
   |cpu
      m4+imem(@1)    // Args: (read stage)
      m4+rf(@2, @3)  // Args: (read stage, write stage) - if equal, no register bypass is required
      m4+dmem(@4)    // Args: (read/write stage)
   
   m4+cpu_viz(@4)    // For visualisation, argument should be at least equal to the last stage of CPU logic
                       // @4 would work for all labs
\SV
   endmodule
```
</details>

<details>

 <summary> Final Implementation</summary>

 ![Screenshot from 2023-08-23 12-04-37](https://github.com/malobimukherjee/RISCV/assets/141206513/ad0c7f33-7d97-450e-a2ad-79296b9eb06b)

</details>
