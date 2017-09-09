# AAS -- ASCII Adjust AL after Subtraction

| Opcode | Instruction | Clocks | Description                       |
| ------ | :---------: | :----: | :-------------------------------: |
| 3F     | AAS         | 4      | ASCII adjust AL after subtraction |

## Operation

```
IF (AL AND 0FH) > 9 OR AF = 1
THEN
   AL := AL - 6;
   AL := AL AND 0FH;
   AH := AH - 1;
   AF := 1;
   CF := 1;
ELSE
   CF := 0;
   AF := 0;
FI;
```

## Description

Execute [AAS](AAS.md) only after a [SUB](SUB.md) instruction that leaves the byte result in the AL register. The lower nibbles of the operands of the [SUB](SUB.md) instruction must have been in the range 0 through 9 (BCD digits). In this case, [AAS](AAS.md) adjusts AL so it contains the correct decimal digit result. If the subtraction produced a decimal carry, the AH register is decremented, and the carry and auxiliary carry flags are set to 1. If no decimal carry occurred, the carry and auxiliary carry flags are set to 0, and AH is unchanged. In either case, AL is left with its top nibble set to 0. To convert AL to an ASCII result, follow the [AAS](AAS.md) with [OR](OR.md) AL, 30H.

## Flags Affected

AF and CF as described above; OF, SF, ZF, and PF are undefined

## Protected Mode Exceptions

None

## Real Address Mode Exceptions

None

## Virtual 8086 Mode Exceptions

None