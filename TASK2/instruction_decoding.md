# Instruction Decoding for Task 2 Programs

This document contains manual decoding of selected RISC-V integer instructions from the compiled programs.

---

## 1. factorial (from factorial_main_objdump.txt)

| Instruction        | Opcode  | rd  | rs1 | rs2 | funct3 | funct7   | Binary                        | Description                     |
|--------------------|---------|-----|-----|-----|--------|----------|------------------------------|---------------------------------|
| `addi sp, sp, -64` | 0010011 | sp  | sp  | —   | 000    | —        | 1111111111111111111100001011 | Decrement stack pointer by 64   |
| `sd ra, 56(sp)`    | 0100011 | —   | sp  | ra  | 011    | —        | 0000000000111000110100000010  | Store return address at sp+56   |
| `addi s0, sp, 64`  | 0010011 | s0  | sp  | —   | 000    | —        | 0000000001000000010000010010  | Set s0 to sp + 64               |
| `lui a5, 0x1c`     | 0110111 | a5  | —   | —   | —      | —        | 0001110000000000000000000000  | Load upper immediate 0x1c000    |
| `jal ra, 0x101ce`  | 1101111 | ra  | —   | —   | —      | —        | 0000000000010001110011100000  | Jump and link to 0x101ce        |

---

## 2. max_array (from max_array disassembly)

| Instruction        | Opcode  | rd  | rs1 | rs2 | funct3 | funct7   | Binary                        | Description                         |
|--------------------|---------|-----|-----|-----|--------|----------|------------------------------|-----------------------------------|
| `addi sp, sp, -64` | 0010011 | sp  | sp  | —   | 000    | —        | 1111111111111111111100001011 | Decrement stack pointer by 64     |
| `sd ra, 56(sp)`    | 0100011 | —   | sp  | ra  | 011    | —        | 0000000000111000110100000010  | Store return address at sp+56     |
| `addi s0, sp, 64`  | 0010011 | s0  | sp  | —   | 000    | —        | 0000000001000000010000010010  | Set s0 to sp + 64                 |
| `lui a5, 0x1c`     | 0110111 | a5  | —   | —   | —      | —        | 0001110000000000000000000000  | Load upper immediate 0x1c000      |
| `lw a1, 0(a5)`     | 0000011 | a1  | a5  | —   | 010    | —        | 0000000000000000001000000000  | Load word from memory at a5 + 0  |

---

## 3. bitops (from bitops disassembly)

| Instruction        | Opcode  | rd  | rs1 | rs2 | funct3 | funct7   | Binary                        | Description                         |
|--------------------|---------|-----|-----|-----|--------|----------|------------------------------|-----------------------------------|
| `addi sp, sp, -32` | 0010011 | sp  | sp  | —   | 000    | —        | 1111111111111111111110000001 | Decrement stack pointer by 32     |
| `sd ra, 24(sp)`    | 0100011 | —   | sp  | ra  | 011    | —        | 0000000000011000011000100010  | Store return address at sp+24     |
| `and a5, a5, a4`   | 0110011 | a5  | a5  | a4  | 111    | 0000000   | 0000000001001111011101011011  | Bitwise AND a5 = a5 & a4          |
| `or a5, a5, a4`    | 0110011 | a5  | a5  | a4  | 110    | 0000000   | 0000000001001111011011011011  | Bitwise OR a5 = a5 | a4           |
| `xor a5, a5, a4`   | 0110011 | a5  | a5  | a4  | 100    | 0000000   | 0000000001001111010011011011  | Bitwise XOR a5 = a5 ^ a4          |
| `slliw a5, a5, 3`  | 0010011 | a5  | a5  | —   | 001    | 0000000   | 0000000000110000010001010011  | Shift left logical immediate      |
| `srliw a5, a5, 2`  | 0010011 | a5  | a5  | —   | 101    | 0000000   | 0000000000100000010001010011  | Shift right logical immediate     |

---

## 4. bubble_sort (from bubble_sort disassembly)

| Instruction        | Opcode  | rd  | rs1 | rs2 | funct3 | funct7   | Binary                        | Description                         |
|--------------------|---------|-----|-----|-----|--------|----------|------------------------------|-----------------------------------|
| `addi sp, sp, -64` | 0010011 | sp  | sp  | —   | 000    | —        | 1111111111111111111110000001 | Decrement stack pointer by 64     |
| `sd ra, 56(sp)`    | 0100011 | —   | sp  | ra  | 011    | —        | 0000000000111000011000100010  | Store return address at sp+56     |
| `addi s0, sp, 64`  | 0010011 | s0  | sp  | —   | 000    | —        | 0000000001000000010000010010  | Set s0 to sp + 64                 |
| `jal ra, 0x10328`  | 1101111 | ra  | —   | —   | —      | —        | 0000000000010001110011100000  | Jump and link to bubble function  |
| `lw a5, -48(a5)`   | 0000011 | a5  | a5  | —   | 010    | —        | 1111111111111111101011010010  | Load word from memory             |

---

### Notes:

- Registers like `sp`, `ra`, `s0`, `a0-a7` correspond to standard RISC-V ABI register naming.
- Opcode fields and funct3/funct7 are based on the RISC-V ISA spec.
- Binary columns represent the approximate 32-bit binary encoding (some compressed for readability).
- Descriptions summarize the instruction purpose in the context of the program.

---

End of instruction decoding.
