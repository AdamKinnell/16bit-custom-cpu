# Registers

16 bits in length.  
12 general purpose registers with usage conventions.  
4 special purpose registers (in **bold**).  
Registers 0 and 15 ignore general-purpose writes.  

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
