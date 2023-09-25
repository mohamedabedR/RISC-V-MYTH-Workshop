# RISC-V-MYTH-Workshop

  This repository includes all the studies and the skills that have beed gained during the [RISC-V based MYTH](https://www.vlsisystemdesign.com/riscv-based-myth/) workshop , that talking about bulding RISC-V piplined core which has support of base interger RV32I using hardware programming langauge called TL-verilog on makerchip platfor

# Table of Contents
- [Day1](##Day1) 
  - [Introduction to RISC-V ISA](###introduction-to-risc-v-isa)
  - [RISC-V software toolchain](###RISC-V-software-toolchain)
  - [Workshop results](###Workshop-results)
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
    
      (risc-v/c program sum.png)
