# Section 3 

# Wave A Flag
This is the first CTF that made me stop and think for a second, but it really shouldn't have been. My first instinct was to `cat` the file, however there was a ton of text that was illegible inside of it. 

There was one line that was legible that said to "pass me a -h" to get the flag. 

So taking this, I ran `./warm -h` which printed out 

`Oh, help? I actually don't do much, but I do have this flag here:`

Final flag: 
`academy{b1scu1ts_4nd_gr4vy_57d8c79}`


# Tab, Tab, Attack
This one is mostly just designed to be annoying. The flag is hidden in an arbitrary file inside of a folder inside of another folder in a Russian nesting doll of random names. 

So I started by unzipping the first folder with `unzip`.

From there I could `ls` and see the next folder, not knowing the whole structure, I used `cd` to enter the folder.

Seeing the continued arbitrary names, I then just used `cd` with tab complete until I went as deep into the file system as possible. That command ended up as:

`cd Ashalmimilkala/Assurnabitashpi/Maelkashishi/Onnissiralis/Ularradallaku/`

From there, `cat fang-of-haynekhtnamet.c` which gave the flag: `academy{l3v3l_up!_t4k3_4_r35t!_9d928112}`
