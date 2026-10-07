# Section 2 (CyberChef)
Now that the foundational skills for connecting to the labs has been established, some basic work can be done. 

# Mod 26
This one focuses on the basics of **cryptography**. Skills learned will be important for future labs.

Using the **CyberChef** website linked in the overview, the user can upload a file to have the contents unencrypted. The file given contains the encrypted text:
`npnqrzl{arkg_gvzr_V'yy_gel_2_ebhaqf_bs_ebg13_5p5s5o36}`.

The assignment mentions ROT13 as the hashing algorithm, so the user can search CyberChef for that algorithm and click "BAKE" if not done automatically. From there, the text should decrypt to the following:
`academy{next_time_I'll_try_2_rounds_of_rot13_5c5f5b36}`

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

# Bases
The prompt asks the user to convert `bDNhcm5fdGgzX3IwcDM1` and mentions something to do with bases. It links **CyberChef** once again, so from there we can input the text into the input field of **CyberChef** and look for the possible base conversions.

Through guessing the different versions of base conversions, you can find the "From Base64" conversion. 

This conversion leads to:
`l3arn_th3_r0p35`

Which when put in the proper format leads the flag to be:
`academy{l3arn_th3_r0p35}`
