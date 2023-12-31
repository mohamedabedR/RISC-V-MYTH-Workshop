# RISC-V-MYTH-Workshop

  This repository includes all the studies and the skills that have beed gained during the [RISC-V based MYTH](https://www.vlsisystemdesign.com/riscv-based-myth/) workshop , that talking about bulding RISC-V piplined core which has support of base interger RV32I using hardware programming langauge called TL-verilog on makerchip platfor

# Table of Contents
- [Day 1](##day-1) 
  - [Introduction to RISC-V ISA](###introduction-to-risc-v-isa)
  - [RISC-V software toolchain](###RISC-V-software-toolchain)
  - [Workshop results](###Workshop-results)
- [Day 2](##day-2)
  - [Introduction to Application Binary Interface (ABI)](###introduction-Application-Binary-Interface-(ABI)) 
- [Day 3](##day-3)
  - [TL-Verilog and Makership](###TL-Verilog-and-Makership)
  - [Combinational logic](###Combinational-logic)
  - [Sequential logic](###Sequential-logic)
  - [Pipelined logic](###Pipelined-logic)
  - [Validity](###Validity)
- [Day 4-5](##day4-5)
   - [Fetch](###Fetch)
   -  [Decode](###Decode)
   - [Register File Read and write](###register-File-Read-and-write)
   -  [Execute](###execute)
   -  [Control Logic](###control-Logic)
   -  [Pipelining the CPU](###pipelining-the-CPU)
   -  [Load and store instructions and memory](###load-and-store-instructions-and-memory)
   -  [Codes](#codes)
- [Acknowledgements](#acknowledgements)

## Day 1
  ### introduction-to-risc-v-isa
  The RISC-V instruction set architecture (ISA) is is an open standard instruction set architecture (ISA) based on established reduced instruction set computer (RISC) principles. Unlike most other ISA designs, RISC-V is provided under royalty-free open-source licenses
  ### RISC-V software toolchain
  there is a several ways for programmers to make and compile and reviwe each code they are programming in linux system .
  1. the simple way and its by using `gcc <file name > ` this command creating for us output file that contains the results .
  2. the Risc-V toolchain witch is not only provide compiler but also have several command that can be useful .
   * risc-v gcc compiler use the below commands:
     
     `riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o <object filename> <C filename>` 
    
      `riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o <object filename> <C filename>`
     
      also it have more options for `-mabi` and `-march`

  * To view assembly code use the below command,
    
     `riscv64-unknown-elf-objdump -d <object filename>`

  * To use SPIKE simualtor to run risc-v obj file use the below command,
  
    `spike pk <object filename>`
    
    To use SPIKE as debugger
    
    `spike -d pk <object Filename>` with degub command as `until pc 0 <pc of your choice>`

     ### Workshop results
      First we programmed a C-code that give us the sum from 1 to n
    
      <img src="risc-v/c program sum.png">

      then we compiled it in the simple way
    
      <img src="risc-v/c program sum results.png">

      the assembly code was

    <img src="risc-v/assm_main.png">

    and if we run the `-Ofast` option of the risc-v gcc compiler we will have
    
    <img src="risc-v/assm_mainf.png">

    and if we use `spike`
    
    <img src="risc-v/runsigned.png">


    
## Day 2
    
  ### introduction Application Binary Interface (ABI)  
  
An Application Binary Interface (ABI) represents a collection of regulations that the Operating System upholds for a particular computing architecture. Consequently, the Linker is responsible for transforming relocatable machine code into absolute machine code by adhering to the ABI interface that aligns with the given machine's architecture.

The system call interface serves as the means through which an application program can interact with architecture-specific registers. In the context of RISC-V architecture, which encompasses 32 or 64 registers, a predefined table outlines the calling convention assigned to these registers, offering application programmers a structured approach for their utilization.

<img src="risc-v/regnames.png">

### Workshop results
the image below contains the `main` code and the `load`
<img src="risc-v/1to9main&load.png">

and then the sum will be :

<img src="risc-v/1to9results.png">

## Day 3
### TL-Verilog and Makership
Our workshop was basicly talkking about buliding a risc-v core so to do it we need a platform , so we used [Makerchip](https://makerchip.com/) it is a free online environment for developing high-quality integrated circuits. by using it we can code,compile,simulate and debug verilog codes . 
This platfrom supports also TL-verilog the used language in this workshop . We will be coding a basic claculator to learn TL-verilog and see how the platform works .

### Combinational logic
First we will start with basic with is the Combinational logic we started with practicing in the not gate `$out = !$in` then we moved to code simple calculator that takes 2 inputs then sum,diff,prod and qout them and the output will be chosen by mux .

<img src="calculator/tlvsimcalc.png">

### Sequential logic
the Sequential logic is basicly the dependency of the inputs on the previous outputs of the design in our code we changed the `$val1[31:0] = rand1[31:0]` to `$val1[31:0] = >>1$out[31:0]` the `>>1` used to indactae to the previous value of any value we need

<img src="calculator/tlvadvcalc.png">

### Pipelined logic

Timing abstract powerful feature of TL-Verilog which converts a code into pipeline stages easily. Whole code under `|pipeline` scope with stages defined by `@?`. 
by divide the code to stages we can run more than one command in the same time witch will be very uselful to for time reduction 

<img src="calculator/pipedclac.png"> 

### Validity

## Day 4-5
Now we can start buliding the RISC-V CPU

### Fetch
the fetch will contain 2 main part :
* The PC that holds the address of next instrtion
* IM Holds the set of instructions

<img src="Risc-v micro/instr.png">

### Decode
This part of code and design maden to differentiate between the diffrent types of Instructions , there is 6 types of instructions 
 * R-type - Register 
 * I-type - Immediate
 * S-type - Store
 * B-type - Branch (Conditional Jump)
 * U-type - Upper Immediate
 * J-type - Jump (Unconditional Jump)
 Also maden to exstract some values existed in the IM like immedate etc.
 
<img src="Risc-v micro/decode1.png">

<img src="Risc-v micro/decode3.png">

<img src="Risc-v micro/decode4.png">

### Register File Read and write
Inputs:
  * Read_Enable   - Enable signal to perform read operation
  * Read_Address1 - Address1 from where data has to be read 
  * Read_Address2 - Address2 from where data has to be read 
  * Write_Enable  - Enable signal to perform write operation
  * Write_Address - Address where data has to be written
  * Write_Data    - Data to be written at Write_Address

Outputs:
  * Read_Data1    - Data from Read_Address1
  * Read_Data2    - Data from Read_Address2

<img src="Risc-v micro/regrd1.png">

<img src="Risc-v micro/regwr.png">


### Execute

<img src="Risc-v micro/alu1.png">

### Control Logic

<img src="Risc-v micro/branch.png">

### Pipelining the CPU
similar to the way we made the simple calculator to stages we had a 3 stages CPU some Images 

<img src="pipelined cpu/start&valid.png">

<img src="pipelined cpu/sourceupdate.png">

<img src="pipelined cpu/branchcorrec.png">

### Load and store instructions and memory

<img src="pipelined cpu/load2.png">

<img src="pipelined cpu/loadstore-test.png">

# Codes

![CPU](codes/CPU.tlv.txt)

![Piplined CPU](codes/pipelinedcpu.tlv.txt)

![load&sotre](codes/load&store.tlv.txt)

![Final form](codes/Last.tlv.txt)


# Acknowledgements
- [Kunal Ghosh](https://github.com/kunalg123), Co-founder, VSD Corp. Pvt. Ltd.
- [Steve Hoover](https://github.com/stevehoover), Founder, Redwood EDA
