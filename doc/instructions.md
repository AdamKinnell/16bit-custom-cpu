# Instructions

There are a total of 27 instructions implemented, which are split into 5 categories.

<img src="https://github.com/AdamKinnell/16bit-custom-cpu/blob/master/img/native_instructions.png">

## Format
Fixed size of 32 bits (2 native 16-bit words) with a fixed format.  
Supports up to 32 *opcodes* with an additional 8 *functions* per opcode.  
Two register fields, *r1* and *r2*, each capable of addressing one of the 16 registers.  
One 16-bit immediate field to directly specify a value in the instruction.  

Each instruction can specify two registers and an immediate value..

The following table shows the number and position of bits corresponding to each field.  
MSB(31) is on the left, and LSB(0) is on the right.

| immediate                             | r2      | r1      | function | opcode    |
|:-------------------------------------:|:-------:|:-------:|:--------:|:---------:|
| 16-bit                                | 4-bit   | 4-bit   | 3-bit    | 5-bit     |
| 15 14 13 12 11 10 9 8 7 6 5 4 3 2 1 0 | 3 2 1 0 | 3 2 1 0 | 2 1 0 | 4 3 2 1 0 |

r1 is also known as *Destination*, as the result is usually stored here.  
r2 is also known as *Source*, as it is usually used as an operand.

Any register may be specified as an operand, including special registers and when r1=r2.  
e.g. you may perform `ADD($t0,$t0)` to get `$t0 = $t0 + $t0`, or `SUB($zero,$t0, 5)` to set the status bits after performing `$t0 - 5` and discarding the result.

The function bits are directly used as the opcode for internal systems.  
Attempting to use unsupported functions will result in undefined behaviour.

## Types
Three different types of instructions are currently supported.  
An RR(C) type instruction could be added in the future.

### RR: Register-Register
Load two operands, each from a register; then store the result in the first register.

>A = r1  
>B = r2  
>Result -> r1

### RI: Register-Immediate
Load two operands, one from a register, and the other as an immediate; then store the result in another register.

>A = r2  
>B = imm  
>Result -> r1

### RI(C): Register-Immediate (Conditional)
Load two operands, one from a register, and the other as an immediate; then store the result in another register, *but only if the compare bit is set*.

>A = r2  
>B = imm  
>Result -> r1, if status[compare]

This type is implemented for all ALU operations (see above) to support conditional expressions such as calculations, moves, and jumps. Such operations can be performed in two instructions, with the first being a comparison operation to set the compare bit.
