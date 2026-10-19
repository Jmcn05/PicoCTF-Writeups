# Problem Set 2 (Part 2)

# First Grep
While we have used grep before, this challenge shows it being used as the base command for the first time rather than just being piped to. 

`grep "academy" file` worked, highlighting the beginning of the flag amongst the rest of the giant string, making it easy to find, but it felt like there must be a way to get it on it's own. More of the intended way.

The man page for `grep` shows the `-o` flag, filtering to only the parts of the file that we know. However, `grep -o "academy" file` would just filter to the word `academy` within the file, not the rest of the flag. 

From a little more research, I figured out that to find an unknown string if you know the start and end of it, you can plug in .* between the two in the filter. So, the final command turns into `grep -o "academy.*} file` because the flag starts with academy and ends with a }.

Making the final flag: `academy{grep_is_good_to_find_things_d00Ca181}`


# First Find
Very simple find command needed to do this one. Nothing beyond that.

Download the attached `.zip` file and extract it. Then, open that directory in a terminal. Please note, if you are using Windows, it is easier to use WSL for this.

Use the find command to locate `uber-secret.txt`.
```
find . -type f -name uber-secret.txt
```
Which provides the file path...
```
./files/adequate_books/more_books/.secret/deeper_secrets/deepest_secrets/uber-secret.txt
```

Simply use `cat` on that file path to read the file which reveals the final flag of `academy{f1nd_15_f457_ab443fd1}`

# Big Zip
Remember that `grep` command from the last section, that's going to be really useful here.

The challenge asks the user to grep through a large amount of files and directories for the flag, very similar to what we did before with the `grep -o` command.

Once in the directory containing all the necessary files, simply type `grep -ro "academy{.*}"`, but let's break down that `-ro`.

- `r` means recursive, so look at the all the files in the directory instead of just one
- `o` means only, just like last time it searches for only the term you have specified and will provide that

So the command recursively searches through all the files for only strings starting with academy{ and ending in }. That gives the final flag of `academy{gr3p_15_m4g1c_ef8790dc}`