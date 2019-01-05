# Registers

16 bits in length.  
16 addressable registers. 
12 general purpose registers with usage conventions.  
4 special purpose registers (in **bold**).  
Registers 0 and 15 ignore general-purpose writes.  

## Usage

| Number | Name    | Comments               |
|--------|---------|------------------------|
| **0**      |**$zero**  | **Always Zero**           |
| 1      | $at     | Assembler Temporary    |
| 2      | $t0     | Temporary              |
| 3      | $t1     | Temporary              |
| 4      | $t2     | Temporary              |
| 5      | $t3     | Temporary              |
| 6      | $t4     | Temporary              |
| 7      | $t5     | Temporary              |
| 8      | $s0     | Saved; Return Address |
| 9      | $ar0    | Argument & Return      |
| 10     | $ar1    | Argument & Return      |
| 11     | $ar2    | Argument & Return      |
| 12     | $ar3    | Argument & Return      |
| **13**     | **$sp**     | **Stack Pointer**          |
| **14**     | **$pc**     | **Program Counter**        |
| **15**    | **$status** | **Status Bits**            |

## Status Register

The bits of the status register ($15/$status) are laid out as follows:

The lower 8 bits of the register are for Status Information from the last execution of an instruction.

| Operation: |   |   |   | ALU  | ALU  | ALU   | ALU      | COMPARE |
|-----------:|:-:|:-:|:-:|:----:|:----:|:-----:|:--------:|:-------:|
| Value:     |   |   |   | zero | sign | carry | overflow | compare |
| Bit #:     | 7 | 6 | 5 | 4    | 3    | 2     | 1        | 0       |

The upper 8 bits are for Error, Exception, and Interrupt information.

| Operation: |    |    |    |    |    |    | MEMORY/PC  | MEMORY/PC |
|-----------:|:--:|:--:|:--:|:--:|:--:|:--:|:----------:|:---------:|
| Value:     |    |    |    |    |    |    | outofrange | unaligned |
| Bit #:     | 15 | 14 | 13 | 12 | 11 | 10 | 9          | 8         |
