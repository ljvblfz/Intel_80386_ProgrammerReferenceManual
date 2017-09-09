# AAM -- ASCII Adjust AX after Multiply

| Opcode | Instruction | Clocks | Description                    |
| ------ | :---------: | :----: | :----------------------------: |
| D4 0A  | AAM         | 17     | ASCII adjust AX after multiply |

## Operation

```
AH := AL / 10;
AL := AL MOD 10;
```

## Description

Execute [AAM](AAM.md) only after executing a [MUL](MUL.md) instruction between two unpacked BCD digits that leaves the result in the AX register. Because the result is less than 100, it is contained entirely in the AL register. [AAM](AAM.md) unpacks the AL result by dividing AL by 10, leaving the quotient (most-significant digit) in AH and the remainder (least-significant digit) in AL.

## Flags Affected

SF, ZF, and PF as described in [Appendix C](../appendix/appc.md); OF, AF, and CF are undefined

## Protected Mode Exceptions

None

## Real Address Mode Exceptions

None

## Virtual 8086 Mode Exceptions

None