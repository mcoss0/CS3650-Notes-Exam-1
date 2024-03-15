
### Examples/Use Cases of MIPS Assembly Instructions

#### 1. `addi` (Add Immediate)
Adding a constant value to a register for adjusting an array index.

```assembly
# Example: Increasing an array index by 4
addi $t0, $t0, 4
```

#### 2. `li` (Load Immediate)
Initializing a register with a specific value at the start of a subroutine.

```assembly
# Example: Setting a loop counter to 10
li $t1, 10
```

#### 3. `lw` (Load Word)
Loading a 32-bit word from memory into a register.

```assembly
# Example: Retrieving the first element of an array
lw $t2, 0($t0)
```

#### 4. `sw` (Store Word)
Storing a 32-bit word from a register back into memory.

```assembly
# Example: Saving a computation result into an array
sw $t2, 4($t0)
```

#### 5. `beq` (Branch if Equal)
Comparing two registers and branching if they are equal.

```assembly
# Example: Loop until $t1 is 0
loop: beq $t1, $zero, end
      # Loop body
      addi $t1, $t1, -1
      j loop
end:   # Exit point
```
