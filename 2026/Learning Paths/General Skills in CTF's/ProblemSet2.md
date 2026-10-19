# Problem Set 2

# Obedient Cat
The flag is hidden in plain sight for anyone to see inside of the file.

On Linux: 
Simply type `cat file` 

On Windows:
Add .txt to the end of the file name and then open it in notepad. 

`academy{s4n1ty_v3r1f13d_61ddac22}`

# Wave A Flag
This is the first CTF that made me stop and think for a second, but it really shouldn't have been. My first instinct was to `cat` the file, however there was a ton of text that was illegible inside of it. 

There was one line that was legible that said to "pass me a -h" to get the flag. 

So taking this, I ran `./warm -h` which printed out 

`Oh, help? I actually don't do much, but I do have this flag here:`

Final flag: 
`academy{b1scu1ts_4nd_gr4vy_57d8c79}`

# convertme.py
The flag for this one appears to be for a basic conversion. Mostly to teach the user how to convert from decimal to binary.

The number it randomly selected for me was `63` which when converted to binary comes out as `111111`.

Technically it should be written as `0b111111`, however when examining the python script it provided, it seemed like it just wanted the value without the leading `0b`.

Upon entering that answer, it provided me with the final flag `academy{4ll_y0ur_b4535_fff0af3d}`.

# what's a net cat?
Connect to `chatelaine.cylabacademy.net` at port `17196` using netcat.

Typically, this would be done using `nc chatelaine.cylabacademy.net 17196`.

However, on Windows, you must type out `ncat chatelaine.cylabacademy.net 17196`. Keep this in mind for future labs where it will assume the user is on Linux and use `nc` instead of `ncat`.

Please note that upon recompleting this CTF, it appears like the URL and port are changed every time, so the answer will vary from instance to instance.

However, it provided the final flag of `academy{nEtCat_Mast3ry_Ed4EE28A}`
