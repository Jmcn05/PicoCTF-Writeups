# The Artificial Neuron


# Neuron Meet 0
A weird one for sure.

This challenge basically gives the user a math formula which you have to make the final output into `01110000` which is ASCII for `p`.

It starts with:
```
Welcome to Neuron Meet 0!
Probe the 1D perceptron to coax out the ASCII for 'p'.
Send a number within the bounds to see if the perceptron fires (1) or stays quiet (0).
- Bounds: [-10.0, 10.0]
- Output rule: w*x + b >= 0 -> 1, else 0.
- No back-to-back repeats of the same number.
- Goal: make the last 8 outputs read 01110000 (ASCII 'p').
- Command: RESET to clear the firing history.
Type HELP for a reminder or EXIT to quit.
```

This doesn't exactly say what `w`, `x`, and `b` are, so let's test it out and see what we can get.
```
[1/128] x> 0
Perceptron stays quiet.
Recent outputs (1/8): 0
[2/128] x> 1
Perceptron stays quiet.
Recent outputs (2/8): 00
[3/128] x> 1
No back-to-back repeats. Pick something different.
[4/128] x> 0
Perceptron stays quiet.
Recent outputs (3/8): 000
[5/128] x> 0
No back-to-back repeats. Pick something different.
[6/128] x> 1
Perceptron stays quiet.
Recent outputs (4/8): 0000
[7/128] x> 0
Perceptron stays quiet.
Recent outputs (5/8): 00000
[8/128] x> 1
Perceptron stays quiet.
Recent outputs (6/8): 000000
[9/128] x> 0
Perceptron stays quiet.
Recent outputs (7/8): 0000000
[10/128] x> 1
Perceptron stays quiet.
Recent outputs (8/8): 00000000
[11/128] x> 0
Perceptron stays quiet.
Recent outputs (8/8): 00000000
```

That's not exactly helpful on the surface, but I did have a theory from this. We can't repeat data, and we know 0 will always output a 0 because we started and ended with that and got 0 all the way.

I thought back to the formula, specificaly the `>= 0 -> 1`. This is when I theorized that our input had to be `>=` the numerator in the counter off to the left in order to output `1`. So I tried applying that theory and ended up doing:
```
[12/128] x> RESET
History cleared. Keep probing the neuron.
[13/128] x> 1
Perceptron stays quiet.
Recent outputs (1/8): 0
[14/128] x> 2
Perceptron fires!
Recent outputs (2/8): 01
[15/128] x> 3
Perceptron fires!
Recent outputs (3/8): 011
[16/128] x> 4
Perceptron fires!
Recent outputs (4/8): 0111
[17/128] x> 0
Perceptron stays quiet.
Recent outputs (5/8): 01110
[18/128] x> 1
Perceptron stays quiet.
Recent outputs (6/8): 011100
[19/128] x> 0
Perceptron stays quiet.
Recent outputs (7/8): 0111000
[20/128] x> 1
Perceptron stays quiet.
Recent outputs (8/8): 01110000
```

The final flag is then given: `academy{n3ur0n_m3t_227803d1}`


# Neuron Meet 2D-0
This follows the same principle as the last one, but with 2 seperate inputs instead of a single one.

Using netcat agian to connect to this challenge, we're greeted with:
```
Welcome to Neuron Meet 2D-0!
Probe the 2D perceptron to coax out the ASCII for 'p'.
Send two numbers (x, y) to see if the perceptron fires (1) or stays quiet (0).
- Bounds: [-10.0, 10.0] for both x and y
- Output rule: w1*x + w2*y + b >= 0 -> 1, else 0.
- No back-to-back repeats of the same (x, y) pair.
- Goal: make the last 8 outputs read 01110000 (ASCII 'p').
- Command: RESET to clear the firing history.
- Format: x,y or x y (comma or space separated)
Type HELP for a reminder or EXIT to quit.
```

Very similar to the previous problem, however this one makes it a little more clear what the inputs actually do because there is `w1` and `w2`. This means your inputs are being mapped to those two points which are added together and then added to some number `b` that is then compared to `0`.

The equation essentially becomes `x + y + b >= 0 -> 1`, so I tested it out:
```
[1/128] (x,y)> 0,0
Perceptron stays quiet.
Recent outputs (1/8): 0
[2/128] (x,y)> 1,2
Perceptron stays quiet.
Recent outputs (2/8): 00
[3/128] (x,y)> 3,4
Perceptron fires!
Recent outputs (3/8): 001
[4/128] (x,y)> 3,4
No back-to-back repeats. Pick a different (x, y) pair.
[5/128] (x,y)> 4,3
Perceptron fires!
Recent outputs (4/8): 0011
[6/128] (x,y)> 5,4
Perceptron fires!
Recent outputs (5/8): 00111
[7/128] (x,y)> 4,5
Perceptron fires!
Recent outputs (6/8): 001111
[8/128] (x,y)> 5,4
Perceptron fires!
Recent outputs (7/8): 0011111
[9/128] (x,y)> 4,5
Perceptron fires!
Recent outputs (8/8): 00111111
[10/128] (x,y)> 5,4
Perceptron fires!
Recent outputs (8/8): 01111111
[11/128] (x,y)> 4,5
Perceptron fires!
Recent outputs (8/8): 11111111
```

This actually made me stop and think, because in my mind he `b` value was supposed to be based on the counter that we see in the `(b/8)`, however if that were the case, we would have gotten a `1` on the second input.

So, I figured `b` had to remain a constant, which made it much easier figure out the algorithm that would work:
```
[12/128] (x,y)> RESET
History cleared. Keep probing the neuron.
[13/128] (x,y)> 0,0
Perceptron stays quiet.
Recent outputs (1/8): 0
[14/128] (x,y)> 4,4
Perceptron fires!
Recent outputs (2/8): 01
[15/128] (x,y)> 5,4
Perceptron fires!
Recent outputs (3/8): 011
[16/128] (x,y)> 4,5
Perceptron fires!
Recent outputs (4/8): 0111
[17/128] (x,y)> 0,0
Perceptron stays quiet.
Recent outputs (5/8): 01110
[18/128] (x,y)> 0,1
Perceptron stays quiet.
Recent outputs (6/8): 011100
[19/128] (x,y)> 0,0
Perceptron stays quiet.
Recent outputs (7/8): 0111000
[20/128] (x,y)> 0,1
Perceptron stays quiet.
Recent outputs (8/8): 01110000
```

Which provides the final flag of: `academy{2d_n3ur0n_m3t_dadc9561}`


# Neuron Express 0
Now we have to solve for the `w` and `b` inputs.

Once connected, we're greeted with:
```
Welcome to Neuron Express 0!
Probe the 1D perceptron, then submit its weight and bias.
Send an integer within the bounds to see if the perceptron fires (1) or stays quiet (0).
- Bounds: [-10, 10]
- Output rule: w*x + b >= 0 -> 1, else 0.
- Command: TEST w b to submit a weight and bias guess.
- The guess must match outputs for every integer x in range.
Type HELP for a reminder or EXIT to quit.
```

That doesn't give us much more information, so let's test a few inputs to see what we get. Basically, we're testing inputs for `x` against what the system expects for `w` and `b` and try and figure out the proper values for `w` and `b` based on that information.
```
[1/128] x> 1
Perceptron stays quiet.
[2/128] x> 2
Perceptron fires!
[3/128] x> 3
Perceptron fires!
[4/128] x> 4
Perceptron fires!
[5/128] x> 5
Perceptron fires!
[6/128] x> 6
Perceptron fires!
[7/128] x> 7
Perceptron fires!
[8/128] x> 8
Perceptron fires!
[9/128] x> 9
Perceptron fires!
[10/128] x> 0
Perceptron stays quiet.
[11/128] x> 10
Perceptron fires!
[12/128] x> 4
Perceptron fires!
[13/128] x> RESET
Not an integer. Try again.
[14/128] x> TEST 2 4
Not quite. The outputs do not match for every integer input.
[15/128] x> TEST 0 0
Not quite. The outputs do not match for every integer input.
[16/128] x> TEST 0 1
Not quite. The outputs do not match for every integer input.
```
This gives a pretty good idea of what we're looking for. From this, I was able to piece together that it was looking for something where the `Perception stays quiet` appears only when `w*x<=1`. The easiest way to do this is to set `w=1` because then the only thing you have to worry about is whether `x<=1`.

So now we basically have the equation `x + b <=0 -> Perception stays quiet. Else, Perception fires!`. This means the only way to get it to "stay quiet" only when `<2` is to set b to `-2`. Therefore, the equation becomes `x - 2 <=0` which is what we're looking for. To get the flag type:
```
TEST 1 -2
```
Which tests the value of `w=1` and `b=-2`. This produces the final flag: `academy{n3ur0n_expr_7b1f1ea2}`


# Neuron Express 2D-0
A little tougher, but nothing impossible once you know the foundation.

Before we begin, let's just go over what we're actually looking for. We're asked to solve for `w1`, `w2`, and `b` in the equation `w1*x + w2*y + b <0`. That's essentially what it boils down to after reading:
```
Welcome to Neuron Express 2D-0!
Probe the 2D perceptron, then submit its weights and bias.
Send two integers (x, y) within the bounds to see if the perceptron fires (1) or stays quiet (0).
- Bounds: [-10, 10] for both x and y
- Output rule: w1*x + w2*y + b >= 0 -> 1, else 0.
- Weights and bias are integers.
- Default command: submit x and y to see whether the perceptron activates.
- Format: x,y or x y (comma or space separated)
- Command: TEST w1 w2 b to submit integer weights and bias.
- The guess must match outputs for every integer (x, y) in range.
```

So, that seems a little confusing, let's test out a few inputs and see what we get as a response.
```
[1/128] (x,y)> 5 4
Perceptron fires!
[2/128] (x,y)> 1 0
Perceptron stays quiet.
[3/128] (x,y)> 1 1
Perceptron stays quiet.
[4/128] (x,y)> 1 2
Perceptron stays quiet.
[5/128] (x,y)> 1 3
Perceptron stays quiet.
[6/128] (x,y)> 1 4
Perceptron stays quiet.
[7/128] (x,y)> 5 1
Perceptron fires!
[8/128] (x,y)> 4 1
Perceptron fires!
[9/128] (x,y)> 3 1
Perceptron fires!
[10/128] (x,y)> 2 1
Perceptron stays quiet.
[11/128] (x,y)> 2 2
Perceptron stays quiet.
[12/128] (x,y)> 2 3
Perceptron stays quiet.
[13/128] (x,y)> 1 0
Perceptron stays quiet.
[14/128] (x,y)> 2 0
Perceptron stays quiet.
[15/128] (x,y)> 3 0
Perceptron fires!
[16/128] (x,y)> 1 1
Perceptron stays quiet.
[17/128] (x,y)> 1 2
Perceptron stays quiet.
[18/128] (x,y)> 2 1
Perceptron stays quiet.
[19/128] (x,y)> 3 1
```

Look closely at those inputs. Any time the first number goes over 3, we get "Perception fires!" back, and any time it's under 3, we get "Perception stays quiet."

It doesn't seem to matter what the input for `y` is, as long as `x` is under 3. This is good to know, because that means `w2` is 0. 

So our current equation comes out to `w1*x + 0y + b < 0` or simpler, `w1*x + b < 0`. Since `x < 3` is the input we're looking for, we can assume the `+ b` is the same a `-3`. So we now have `w2=0` and `b=-3` which for `w1*x - 3 < 0`, where x is also `< 3`, `w1 = 1`.

So to input this, we can use `TEST` to get our flag. `TEST 1 0 -3` give the final flag `academy{n3ur0n_expr_2d_0159e40e}`