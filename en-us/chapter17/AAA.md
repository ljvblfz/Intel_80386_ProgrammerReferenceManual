# AAA -- ASCII Adjust after Addition

| Opcode | Instruction | Clocks | Description                    |
| ------ | :---------: | :----: | :----------------------------: |
| 37     | AAA         | 4      | ASCII adjust AL after addition |

## Operation

```
IF ((AL AND 0FH) > 9) OR (AF = 1)
THEN
   AL := (AL + 6) AND 0FH;
   AH := AH + 1;
   AF := 1;
   CF := 1;
ELSE
   CF := 0;
   AF := 0;
FI;
```

## Description

Execute [AAA](AAA.md) only following an [ADD](ADD.md) instruction that leaves a byte result in the AL register. The lower nibbles of the operands of the [ADD](ADD.md) instruction should be in the range 0 through 9 (BCD digits). In this case, [AAA](AAA.md) adjusts AL to contain the correct decimal digit result. If the addition produced a decimal carry, the AH register is incremented, and the carry and auxiliary carry flags are set to 1. If there was no decimal carry, the carry and auxiliary flags are set to 0 and AH is unchanged. In either case, AL is left with its top nibble set to 0. To convert AL to an ASCII result, follow the [AAA](AAA.md) instruction with [OR](OR.md) AL, 30H.

## Flags Affected

AF and CF as described above; OF, SF, ZF, and PF are undefined

## Protected Mode Exceptions

None

## Real Address Mode Exceptions

None