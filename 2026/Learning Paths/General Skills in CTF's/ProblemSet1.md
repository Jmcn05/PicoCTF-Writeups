# Problem Set 1

# Lets Warm Up
The challenge just asks you to convert Hexidecimal to ASCI. 

The Hex code `0x70` 

First, remove the `0x` from the hex code, then take digits `70` and seperate them to convert to decimal. 

7 x 1<sup>1</sup> = 112

0 x 16<sup>0</sup> = 0

This comes out to `112 + 0` or `112`.

112 on the ASCI table maps to `p`, so the final flag is `academy{p}`

# Warmed Up
The challenge doesn't link a website or give instructions to connect to anything this time. It simply asks:
`What is 0x3D (base 16) in decimal (base 10)?`

To convert 3D to decimal, first take the two separate digits.
```
3 = 3
D = 13
```
So, with those values, assign positions from right to left starting with 0, then multiply the digit by 16^x with x being that position.
13 x 16<sup>0</sup> = 13

3 x 16<sup>1</sup> = 48

Finally, add those digits together
`13 + 48 = 61`

So the final flag is 
`academy{61}

# 2warm
This part asks you to convert a value from decimal to binary. The value given is `42`, so to make it easier, start with seperating the digits.

```
2
40
```
The rules of binary state that starting with 0, every number can be either 0 or 1. So the order goes

(128)(64)(32)(16) (8)(4)(2)(1)

With each number in the () being the maximum value of that position. So for example

`0101 = 5`

Going back to our example:
```
2 = 0010
40 = 0010 1000
```
So the final conversion is 00101010.

While traditionally you would leave the leading 0s, the flag does not. So the final flag is:
`academy{101010}
