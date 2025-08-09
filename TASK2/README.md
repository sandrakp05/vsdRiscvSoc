# RISC-V Task 2: Prove Your Local RISC-V Setup
TASK 2.1 -SET UP UNIQUE IDENTITY VARIABLES
export U=$(id -un)
export H=$(hostname -s)
export M=$(head -c 16 /etc/machine-id)
export T=$(date -u +%Y-%m-%dT%H:%M:%SZ)
export E=$(date +%s)

OUTPUT:

<img width="686" height="133" alt="Screenshot from 2025-08-10 00-17-18" src="https://github.com/user-attachments/assets/58e6967d-39f9-442c-ab77-fb1b64e3c35f" />

# factorial.c

riscv64-unknown-elf-gcc -O0 -g -march=rv64imac -mabi=lp64 \
-DUSERNAME="\"$U\"" -DHOSTNAME="\"$H\"" -DMACHINE_ID="\"$M\"" \
-DBUILD_UTC="\"$T\"" -DBUILD_EPOCH=$E \
factorial.c -o factorial

spike pk ./factorial


<img width="690" height="242" alt="Screenshot from 2025-08-10 00-24-14" src="https://github.com/user-attachments/assets/26607576-c6fc-4b07-8269-974336e5332d" />

OUTPUT:
<img width="794" height="529" alt="Screenshot from 2025-08-10 00-38-28" src="https://github.com/user-attachments/assets/cf8469bf-8718-4b77-8501-cfe4b174a179" />


# max_array.c
riscv64-unknown-elf-gcc -O0 -g -march=rv64imac -mabi=lp64 \
-DUSERNAME="\"$U\"" -DHOSTNAME="\"$H\"" -DMACHINE_ID="\"$M\"" \
-DBUILD_UTC="\"$T\"" -DBUILD_EPOCH=$E \
max_array.c -o max_array

spike pk ./max_array

<img width="690" height="242" alt="Screenshot from 2025-08-10 00-32-14" src="https://github.com/user-attachments/assets/feb1f17d-3211-442a-9ff5-bd4be496d1d6" />

OUTPUT:
<img width="792" height="720" alt="Screenshot from 2025-08-10 00-39-48" src="https://github.com/user-attachments/assets/562d9e32-30b9-45f3-9ece-438007cd63a8" />
<img width="778" height="450" alt="Screenshot from 2025-08-10 00-40-06" src="https://github.com/user-attachments/assets/1baa217b-0f26-46eb-ba61-e0889a2918e0" />


# bubble_sort.c
riscv64-unknown-elf-gcc -O0 -g -march=rv64imac -mabi=lp64 \
-DUSERNAME="\"$U\"" -DHOSTNAME="\"$H\"" -DMACHINE_ID="\"$M\"" \
-DBUILD_UTC="\"$T\"" -DBUILD_EPOCH=$E \
bubble_sort.c -o bubble_sort

spike pk ./bubble_sort

<img width="690" height="242" alt="Screenshot from 2025-08-10 00-34-26" src="https://github.com/user-attachments/assets/db3999a2-8861-4577-85b2-5b7ff30505dc" />

OUTPUT:
<img width="794" height="688" alt="Screenshot from 2025-08-10 00-41-45" src="https://github.com/user-attachments/assets/c5e8de1a-a6e6-4f34-bfb5-46ceb3d4eb61" />

<img width="793" height="465" alt="Screenshot from 2025-08-10 00-42-06" src="https://github.com/user-attachments/assets/6b962a96-76a4-4040-803e-1f9a2daa4b63" />

# bitops.c
riscv64-unknown-elf-gcc -O0 -g -march=rv64imac -mabi=lp64 \
-DUSERNAME="\"$U\"" -DHOSTNAME="\"$H\"" -DMACHINE_ID="\"$M\"" \
-DBUILD_UTC="\"$T\"" -DBUILD_EPOCH=$E \
bitops.c -o bitops

spike pk ./bitops

<img width="690" height="313" alt="Screenshot from 2025-08-10 00-35-25" src="https://github.com/user-attachments/assets/c37ee30c-ae72-44ce-a679-bb7cf8abbc6e" />

OUTPUT:

<img width="1025" height="659" alt="Screenshot from 2025-08-10 00-44-15" src="https://github.com/user-attachments/assets/fa2d5cd3-3b93-4f18-8ee9-3ed28e06f6f5" />

<img width="792" height="508" alt="Screenshot from 2025-08-10 00-44-55" src="https://github.com/user-attachments/assets/1cfdeb62-2b9b-4adb-80ce-c0dcc1943445" />

#INSTRUCTION DECODING

Manually decoded at least 5 RISC-V instructions



[instruction_decoding.md](https://github.com/user-attachments/files/21701135/instruction_decoding.md)
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

