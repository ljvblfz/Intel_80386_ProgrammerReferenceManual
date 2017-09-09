# ADC -- Add with Carry

| Opcode   | Instruction     | Clocks | Description                                             |
| -------- | :-------------: | :----: | :-----------------------------------------------------: |
| 14 ib    | ADC AL,imm8     | 2      | Add with carry immediate byte to AL                     |
| 15 iw    | ADC AX,imm16    | 2      | Add with carry immediate word to AX                     |
| 15 id    | ADC EAX,imm32   | 2      | Add with carry immediate dword to EAX                   |
| 80 /2 ib | ADC r/m8,imm8   | 2/7    | Add with carry immediate byte to r/m byte               |
| 81 /2 iw | ADC r/m16,imm16 | 2/7    | Add with carry immediate word to r/m word               |
| 81 /2 id | ADC r/m32,imm32 | 2/7    | Add with CF immediate dword to r/m dword                |
| 83 /2 ib | ADC r/m16,imm8  | 2/7    | Add with CF sign-extended immediate byte to r/m word    |
| 83 /2 ib | ADC r/m32,imm8  | 2/7    | Add with CF sign-extended immediate byte into r/m dword |
| 10 /r    | ADC r/m8,r8     | 2/7    | Add with carry byte register to r/m byte                |
| 11 /r    | ADC r/m16,r16   | 2/7    | Add with carry word register to r/m word                |
| 11 /r    | ADC r/m32,r32   | 2/7    | Add with CF dword register to r/m dword                 |
| 12 /r    | ADC r8,r/m8     | 2/6    | Add with carry r/m byte to byte register                |
| 13 /r    | ADC r16,r/m16   | 2/6    | Add with carry r/m word to word register                |
| 13 /r    | ADC r32,r/m32   | 2/6    | Add with CF r/m dword to dword register                 |

## Operation

```
DEST := DEST + SRC + CF;
```

## Description

[ADC](ADC.md) performs an integer addition of the two operands DEST and SRC and the carry flag, CF. The result of the addition is assigned to the first operand (DEST), and the flags are set accordingly. [ADC](ADC.md) is usually executed as part of a multi-byte or multi-word addition operation. When an immediate byte value is added to a word or doubleword operand, the immediate value is first sign-extended to the size of the word or doubleword operand.

## Flags Affected

OF, SF, ZF, AF, CF, and PF as described in [Appendix C](../appendix/appc.md)

## Protected Mode Exceptions

`#GP(0)` if the result is in a nonwritable segment; `#GP(0)` for an illegal memory operand effective address in the CS, DS, ES, FS, or GS segments; `#SS(0)` for an illegal address in the SS segment; `#PF(fault-code)` if page fault

## Real Address Mode Exceptions

Interrupt 13 if any part of the operand would lie outside of the effective address space from 0 to 0FFFFH

## Virtual 8086 Mode Exceptions

Same exceptions as in Real Address Mode; `#PF(fault-code)` for a page fault