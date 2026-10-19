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

From there, `cat fang-of-haynekhtnamet.c` which gave the flag: `academy{l3v3l_up!_t4k3_4_r35t!_9d928112}`.


# Insp3ct0r
This one splits the flag into thirds for the user to find. 

The first third can be found in the page source code. The HTML holds a comment saying:
`<!-- Html is neat. Anyways have 1/3 of the flag: academy{tru3_d3 -->`

The second third can be found in the mycss.css file which is linked in the page source code. View page source and then click the file hyperlink to find it easily.
`You need CSS to make pretty pages. Here's part 2/3 of the flag: t3ct1ve_0r_ju5t`

The final third of the flag can be found in the myjs.js file which is linked in the page source code. View the page source and then click the file hyperlink to find it easily.
`Javascript sure is neat. Anyways part 3/3 of the flag: _lucky?aa3ae7c8}`

Therefore, the final flag can be pieced together as: `academy{tru3_d3t3ct1ve_0r_ju5t_lucky?aa3ae7c8}`


# strings it
strings it was one of the few that took me a bit of time to figure out. My initial instinct was to use `cat strings | grep "academy" ` to find it, but that didn't work.

That returned `grep: (standard input): binary file matches` and there was no flags that worked properly that I could find to solve the challenge without printing the entire file.

So back to square one, I attempted to then use the `strings` command. Combined with `grep`, it found the flag. So `strings strings | grep "academy"` returned the flag `academy{5tRIng5_1T_d47eAaCB}`

# First Grep
While we have used grep before, this challenge shows it being used as the base command for the first time rather than just being piped to. 

`grep "academy" file` worked, highlighting the beginning of the flag amongst the rest of the giant string, making it easy to find, but it felt like there must be a way to get it on it's own. More of the intended way.

The man page for `grep` shows the `-o` flag, filtering to only the parts of the file that we know. However, `grep -o "academy" file` would just filter to the word `academy` within the file, not the rest of the flag. 

From a little more research, I figured out that to find an unknown string if you know the start and end of it, you can plug in .* between the two in the filter. So, the final command turns into `grep -o "academy.*} file` because the flag starts with academy and ends with a }.

Making the final flag: `academy{grep_is_good_to_find_things_d00Ca181}`

# Where are the robots
The instructions for this challenge are intentionally vague, not really showing anything for the user to work off of. That actually made it quite a struggle, and my first thought was to go the the page source code and search through that for the answer.

However, the page source left nothing for except a css file which was only a dead end. 

My next thought was to search for subdirectories for the web page, adding `/index.html` `/index/` and eventually `/robots.txt` onto the end. I don't know if there was an easier way to find this or not, but I eventually did. This find led me to add `/47a0d.html` onto the end of my search, revealing the final flag.

The flag then was `academy{ca1cu1at1ng_Mach1n3s_47a0d}`

I feel like this one should have told you to search for a .txt file or something, it didn't seem to have a clear direction. I could have pulled out all of the web penetration testing tools I've used from PortSwigger labs, but I wanted to keep with only the intentional way of doing the challenge.
