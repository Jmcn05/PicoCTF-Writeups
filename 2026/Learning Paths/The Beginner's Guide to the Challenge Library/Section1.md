# Section 1 (Sanity)
Section 1 goes of the very basics of how CTFs work and what to expect. It builds the foundational knowledge for the user to work off of in future challenges.

# Obedient Cat
The flag is hidden in plain sight for anyone to see inside of the file.

On Linux: 
Simply type `cat file` 

On Windows:
Add .txt to the end of the file name and then open it in notepad. 

`academy{s4n1ty_v3r1f13d_61ddac22}`

# Super SSH
Super SSH requires the user to actually connect to a machine. Open a terminal and ssh in using the provided credentials.

Once connected, the ssh session automatically ends and provides the flag automatically. 

`academy{s3cur3_c0nn3ct10n_eb2040c5}`

# what's a net cat?
Connect to `chatelaine.cylabacademy.net` at port `17196` using netcat.

Typically, this would be done using `nc chatelaine.cylabacademy.net 17196`.

However, on Windows, you must type out `ncat chatelaine.cylabacademy.net 17196`. Keep this in mind for future labs where it will assume the user is on Linux and use `nc` instead of `ncat`.
