# Design Decisions

## Comparison Operations
8 native comparison operations are provided.
The result of the comparison is stored in the Compare bit of the status register for later use.
All 8 operands are of the form:
> A : Register
> B : Register or Immediate

GT (>) and GTU (>) are able to be calculated in a single instruction using one of the other 6 operations, however this is only possible with two register operands.
These two instructions allow Greater-Than comparisons with immediate operands.

As the Greater-Than comparisons are primarily for use with immediate operands, it was decided to leave out GTE (>=) and GTEU (>=), as the immediate can simply be decreased by 1.

## Instruction Types

At first, we had following design:

**	Instruction Formats:**
Fixed size of 16 bits.
Up to 32 native instructions.
Up to 8 possible functions per opcode.
Up to 16 addressable general-purpose registers.

**	Register-Type (R)**
Two 4-bit registers and 3-bit function / operation type.

| opcode | reg1  | reg2  | function |
|--------|-------|-------|----------|
| 5-bit  | 4-bit | 4-bit | 3-bit    |

**	Immediate-Type (I)**
One 3-bit register and sign-extended 8-bit operand.
Only the lower 8 registers can be addressed by this instruction type.

| opcode | reg1  | imm   |
|--------|-------|-------|
| 5-bit  | 3-bit | 8-bit |

Later, the decision was made to move to a single 32-bit instruction type in order to
simplify design and implementation, as well as enable a wider variety of instructions.

## Pass-Through Operations

The lower 8 opcodes will result in the function field of the instruction being passed directly as an input to one of the processors internal modules. This simplifies implementation by reducing the complexity of the CPU control module, allows a wider variety of operations to be performed, and helps to abstract the implementation of various operations which are processed directly by an internal module.

The first operand to the module is always the value in a specified register (r1), while the second operand can be either the value in a second specified register (r2) or the immediate operand specified in the instruction.

An even opcode specifies register, while an odd opcode specifies immediate.

This design greatly simplifies the implementation of common operations that work with either immediate or register operands.

## Native Instructions

Some instructions were implemented natively, so as to be performed in a single cycle. This may be due to ease of implementation or the assessment that the operation may be commonly performed.

Other instructions were not implemented natively due to being:
* Possible with an existing native instruction, or
* Uncommon enough to warrant the extra cycles, or
* Too complicated or time consuming, or
* Simply not necessary.

**Examples:**

* LI (load immediate)
Any of: AND $rd, $0, imm ; OR $rd, $0, imm ; etc.
* LUI (load upper immediate)
Unnecessary, as instruction format holds full 16-bit immediate.

## No Native Control Transfer Instructions

There are no native control transfer instructions in this instruction set, such as jump or branch. Instead, other primitive operations may be used to achieve the same result (in one clock cycle).

This is possible due to PC being usable as a general-purpose register.

**Jump Register**
>(RR) ADD $pc, $zero, $reg

**Jump Immediate/Label**
>(RI) ADD, $pc, $zero, imm

**Jump PC-Relative**
>(RI) ADD $pc, $pc, imm

**Branch Register (Conditional)**
>(RIC) OR $pc, $reg, 0

**Branch Immediate/Label (Conditional)**
>(RIC) OR $pc, $zero, imm

**Branch PC-Relative (Conditional)**
>(RIC) ADD $pc, $pc, imm
