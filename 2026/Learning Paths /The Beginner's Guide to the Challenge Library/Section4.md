# Python Wrangling 
This first challenge wants the user to find the flag using only one line. Invoking the given python script and forwarding the password from the `.txt` file should solve it.

The following command puts it all into one line, although there are several ways of doing this.
```
python3 ende.py -d flag.txt.en < password.txt
```
So the final flag is `academy{4p0110_1n_7h3_h0us3_d6af8f37}`.

# PW Crack 1
This lab asks the user to execute the python script to find the password within the `level1.flag.txt.enc` file.

First, understand what the python file actually says. Run `cat level1.py` to find the code
```
### THIS FUNCTION WILL NOT HELP YOU FIND THE FLAG --LT ########################
def str_xor(secret, key):
    #extend key to secret length
    new_key = key
    i = 0
    while len(new_key) < len(secret):
        new_key = new_key + key[i]
        i = (i + 1) % len(key)
    return "".join([chr(ord(secret_c) ^ ord(new_key_c)) for (secret_c,new_key_c) in zip(secret,new_key)])
###############################################################################


flag_enc = open('level1.flag.txt.enc', 'rb').read()



def level_1_pw_check():
    user_pw = input("Please enter correct password for flag: ")
    if( user_pw == "691d"):
        print("Welcome back... your flag, user:")
        decryption = str_xor(flag_enc.decode(), user_pw)
        print(decryption)
        return
    print("That password is incorrect")



level_1_pw_check()
```
The important thing here is the hard-coded password which is needed to execute the file. Unlike the last flag, this one cannot be done by forwarding another file into it, though if you wanted to you could run `< 691d`

But doing it in separate lines gives you the complete command `python3 level1.py` with output 
```
Please enter correct password for flag: 691d
Welcome back... your flag, user:
academy{545h_r1ng1ng_329bb7f6}
```
Therefore, the flag is `academy{545h_r1ng1ng_329bb7f6}`


# PW Crack 2
The second PW Crack makes you figure out what the password to the password cracker is. 

Similar to the last one, you can `cat` the file and find
```
### THIS FUNCTION WILL NOT HELP YOU FIND THE FLAG --LT ########################
def str_xor(secret, key):
    #extend key to secret length
    new_key = key
    i = 0
    while len(new_key) < len(secret):
        new_key = new_key + key[i]
        i = (i + 1) % len(key)
    return "".join([chr(ord(secret_c) ^ ord(new_key_c)) for (secret_c,new_key_c) in zip(secret,new_key)])
###############################################################################

flag_enc = open('level2.flag.txt.enc', 'rb').read()



def level_2_pw_check():
    user_pw = input("Please enter correct password for flag: ")
    if( user_pw == chr(0x33) + chr(0x39) + chr(0x63) + chr(0x65) ):
        print("Welcome back... your flag, user:")
        decryption = str_xor(flag_enc.decode(), user_pw)
        print(decryption)
        return
    print("That password is incorrect")



level_2_pw_check()
```
Take a close look at that password requirement, unlike last time it's not written in plaintext, but it is hard-coded. 
`chr(0x33) + chr(0x39) + chr(0x63) + chr(0x65)` actually is hexadecimal format for `39ce`. Running the file and entering that as the password, the CTF flag is given:

```
Please enter correct password for flag: 39ce
Welcome back... your flag, user:
academy{tr45h_51ng1ng_82234aa4}
```

