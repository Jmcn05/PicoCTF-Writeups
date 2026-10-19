# Problem Set 1 (Part 2)

# Nice netcat...
The CTF provides a very straightforward problem to solve.

It provides a simple `netcat` command, the same way that previous flags have been found. Upon typing in that command, `nc chatelaine.cylabacademy.net 24098`, it provides a large string of numbers.
```
97
99
97
100
101
109
121
123
103
48
48
100
95
107
49
116
116
121
33
95
110
49
99
51
95
107
49
116
116
121
33
95
55
101
102
53
50
125
10
```
When you convert this string of numbers into text using an ASCII table, it comes out with the final flag of `academy{g00d_k1tty!_n1c3_k1tty!_7ef52}`.

# Tab, Tab, Attack
This one is mostly just designed to be annoying. The flag is hidden in an arbitrary file inside of a folder inside of another folder in a Russian nesting doll of random names. 

So I started by unzipping the first folder with `unzip`.

From there I could `ls` and see the next folder, not knowing the whole structure, I used `cd` to enter the folder.

Seeing the continued arbitrary names, I then just used `cd` with tab complete until I went as deep into the file system as possible. That command ended up as:

`cd Ashalmimilkala/Assurnabitashpi/Maelkashishi/Onnissiralis/Ularradallaku/`

From there, `cat fang-of-haynekhtnamet.c` which gave the flag: `academy{l3v3l_up!_t4k3_4_r35t!_9d928112}`.

# Python Wrangling 
This first challenge wants the user to find the flag using only one line. Invoking the given python script and forwarding the password from the `.txt` file should solve it.

The following command puts it all into one line, although there are several ways of doing this.
```
python3 ende.py -d flag.txt.en < password.txt
```
So the final flag is `academy{4p0110_1n_7h3_h0us3_d6af8f37}`.

# Magikarp Ground Mission
This one was a fun one, but I don't really understand the naming of it. It was just a normal `ssh` into the session and finding the flags.

Start by using `ssh` into the provided IP and port. For me it was `ssh -p 39393 ctf-player@chatelaine.cylabacademy.net`

Once in, use `ls` to view the files. You can see 2 files, `1of3.flag.txt`  `instructions-to-2of3.txt`. So, use `cat` to find the answer inside of `1of3.flag.txt` and then view the instructions for the next part of the flag. 
```
cat 1of3.flag.txt
academy{xxsh_

cat instructions-to-2of3.txt
Next, go to the root of all things, more succinctly `/`
```

Use the provided instructions to find your way to the root directory. Use `cd /` to move there. Another `ls` shows 2 more important files, `2of3.flag.txt` and instructions for part 3. 
```
cat 2of3.flag.txt
0ut_0f_//4t3r_

cat instructions-to-3of3.txt
Lastly, ctf-player, go home... more succinctly `~`
```

So, the final part of the flag is in the home directory. Use `cd ~` to get there.
```
cat 3of3.flag.txt
47c47679}
```

Putting it all together, the final flag is revealed as `academy{xxsh_0ut_0f_//4t3r_47c47679}`