# Multiplication
We can design a multiplier with two ways one of them is combinational which has better performance but required more chip area, and other one is sequential which gain its power reuse the hardware again and again in process and can be reach high clock frequency with the help of pipeline.

## Sequential Multiplier
Lets we think about long multiplication in binary.
- Sequential binary multiplication of 10111 and 10011:

            00010111 --> multiplicand
        x   00010011 --> multiplier
        _________________
            00000000
             00000000
              00000000
               00010111
                00000000
                 00000000
                  00010111
        +          00010111
        _________________
               000110110101 --> product

As usual, we can start multiplication from left to right, but in binary we can use rigth to left as an alternative because there is no carry in this state.

We need to multiply this two number and every bits of second number should be multiplied and their shifted state will summed as a result.

But this method behave like unsigned operation. Therefor we need to determine sign of operation and then we need to make some extra step to complete.

1- First step is determine the resulting product sign.
```systemverilog
assign sign = A[XLEN-1] ^ B[XLEN-1];
```

2- Second step will be take absolute value of operant to obtain proper result in binary.

Lets we have -5

   binary representation :

   ```
   -5:  11011
   ```

Two's complement gives absolute (corresponding positive) number in sort.
   ```
   |-5| : 00100 (not equal still)
   ```
Then add 1 to it

   ```
   |-5| : 00100 + 00001 = 00101
   ```

3 - Now multiply two number using algorithm.

    a. First thing if you multiply two 32 bit value you obtain at most a 64-bit number. It means you need 32 bit two operant and 64 bit product output.

    b. While multiplying every bit of the second number with first number we need to count how many bit is multiplied to ensure when process will end. So there shoul be an counter for this.

    c. To iterate on second number bits simply we can shift number.

    d.
        - First operant is called multiplicand
        - Second operant is called multiplier

    e. There should be multiplier register to hold value of B.
        - We also use this register to hold shifted value to optimize total number of register used in design.

    f. Lastly, we need a product register to hold the result of every cycle until final result will obtained.

    g. When counter shows last bit is iterated process will done.

    The core code of operation is done in two important code block below

```systemverilog
mult    <= mult << 1;   // shift one bit mult in every cycle to iterate its most significant bit previous index
prod    <= (prod + (A & {SIZE{mult[SIZE-1]}})) << shift; // multiply in one bit number with n bit A same operation with logical AND. If coming bit mult is one so copy A to new block of summution operation by shifting it in every block place. In case of bit mult is zero is equalt logical AND 0 whole number(result will zero array).
```

instead of this code block as I mentioned earlier we can use rigth shift to get rid of mul register and reduce the addition operation to 32 bit from 64 bit.

```systemverilog
/*
ex
    A = 3'b010  = 2   Multiplicand
    B = 3'b101  = 5   Multiplier
  X------------
           010
          000
         010
  +------------
         01010   = 10 Product

  0 => place 0      (0 x multiplicand)
  1 => place a copy (1 x multiplicand)



010 101 start

010 + (010 & 111) = 100
prod   = 100 101
shift0 = 010 010

010 + (010 & 000) = 010
prod   = 010 010
shift1 = 001 001

001 + (010 & 111) = 011
prod   = 011 001
shift2 = 001 100 = 10


*/
```