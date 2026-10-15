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

# PW Crack 3
When you download the files, you're given a python file with a hashing algorithm asking for a password. A list of passwords is provided at the bottom of the file as seen below.
```
import hashlib

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

flag_enc = open('level3.flag.txt.enc', 'rb').read()
correct_pw_hash = open('level3.hash.bin', 'rb').read()


def hash_pw(pw_str):
    pw_bytes = bytearray()
    pw_bytes.extend(pw_str.encode())
    m = hashlib.md5()
    m.update(pw_bytes)
    return m.digest()


def level_3_pw_check():
    user_pw = input("Please enter correct password for flag: ")
    user_pw_hash = hash_pw(user_pw)
    
    if( user_pw_hash == correct_pw_hash ):
        print("Welcome back... your flag, user:")
        decryption = str_xor(flag_enc.decode(), user_pw)
        print(decryption)
        return
    print("That password is incorrect")



level_3_pw_check()


# The strings below are 7 possibilities for the correct password. 
#   (Only 1 is correct)
pos_pw_list = ["6997", "3ac8", "f0ac", "4b17", "ec27", "4e66", "865e"]
```

While this may seem intimidating, let's break it down into a few different sections that we can analyze. 
```
def hash_pw(pw_str):
    pw_bytes = bytearray()
    pw_bytes.extend(pw_str.encode())
    m = hashlib.md5()
    m.update(pw_bytes)
    return m.digest()
```
This says that whatever input is given to the function will be hashed and returned to wherever called it.

```
def level_3_pw_check():
    user_pw = input("Please enter correct password for flag: ")
    user_pw_hash = hash_pw(user_pw)
    
    if( user_pw_hash == correct_pw_hash ):
        print("Welcome back... your flag, user:")
        decryption = str_xor(flag_enc.decode(), user_pw)
        print(decryption)
        return
    print("That password is incorrect")
```
This function is very similar to other ones seen in other CTFs. Basically, it asks the user for an input and checks if that's the expected input. This time however, it asks the user for an input, then hashes that input and checks it against the file that holds the password. 

Finally, we're given the list below
```
pos_pw_list = ["6997", "3ac8", "f0ac", "4b17", "ec27", "4e66", "865e"]
```

So now, we can take the program and alter it slightly. The goal is to automate it running through the password list until the correct one is found and then returning the flag. While we could in theory just input each of the potential passwords, the more important exercise is to automate it to be expanded later.

The only part changed is the `def level_3_pw_check():`. This way of doing it defines the list ahead of time, then automates running through that list until the correct password is found, continuing on from there.
```
def level_3_pw_check():
    pos_pw_list = [
        "6997", "3ac8", "f0ac", "4b17", "ec27", "4e66", "865e"
    ]

    for user_pw in pos_pw_list:
        user_pw_hash = hash_pw(user_pw)

        if user_pw_hash == correct_pw_hash:
            print("Correct password:", user_pw)
            print("Welcome back... your flag, user:")

            decryption = str_xor(flag_enc.decode(), user_pw)
            print(decryption)
            return

    print("No matching password found.")
```
So the final flag is `academy{m45h_fl1ng1ng_b8034615}`

# PW Crack 4
This follows almost the exact same principles as the previous CTF. So, opening up the `.py` file, we can see:
```
import hashlib

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

flag_enc = open('level4.flag.txt.enc', 'rb').read()
correct_pw_hash = open('level4.hash.bin', 'rb').read()


def hash_pw(pw_str):
    pw_bytes = bytearray()
    pw_bytes.extend(pw_str.encode())
    m = hashlib.md5()
    m.update(pw_bytes)
    return m.digest()


def level_4_pw_check():
    user_pw = input("Please enter correct password for flag: ")
    user_pw_hash = hash_pw(user_pw)

    if( user_pw_hash == correct_pw_hash ):
        print("Welcome back... your flag, user:")
        decryption = str_xor(flag_enc.decode(), user_pw)
        print(decryption)
        return
    print("That password is incorrect")



level_4_pw_check()



# The strings below are 100 possibilities for the correct password.
#   (Only 1 is correct)
pos_pw_list = ["6288", "6152", "4c7a", "b722", "9a6e", "6717", "4389", "1a28", "37ac", "de4f", "eb28", "351b", "3d58", "948b", "231b", "973a", "a087", "384a", "6d3c", "9065", "725c", "fd60", "4d4f", "6a60", "7213", "93e6", "8c54", "537d", "a1da", "c718", "9de8", "ebe3", "f1c5", "a0bf", "ccab", "4938", "8f97", "3327", "8029", "41f2", "a04f", "c7f9", "b453", "90a5", "25dc", "26b0", "cb42", "de89", "2451", "1dd3", "7f2c", "8919", "f3a9", "b88f", "eaa8", "776a", "6236", "98f5", "492b", "507d", "18e8", "cfb5", "76fd", "6017", "30de", "bbae", "354e", "4013", "3153", "e9cc", "cba9", "25ea", "c06c", "a166", "faf1", "2264", "2179", "cf30", "4b47", "3446", "b213", "88a3", "6253", "db88", "c38c", "a48c", "3e4f", "7208", "9dcb", "fc77", "e2cf", "8552", "f6f8", "7079", "42ef", "391e", "8a6d", "2154", "d964", "49ec"]
```

That's a lot more flags to guess and check, so this is when it's important to have that automated script from before.

So, changing the `level_4_pw_check()` function, it then becomes:
```
def level_4_pw_check():
    pos_pw_list = ["6288", "6152", "4c7a", "b722", "9a6e", "6717", "4389", "1a28", "37ac", "de4f", "eb28", "351b", "3d58", "948b", "231b", "973a", "a087", "384a", "6d3c", "9065", "725c", "fd60", "4d4f", "6a60", "7213", "93e6", "8c54", "537d", "a1da", "c718", "9de8", "ebe3", "f1c5", "a0bf", "ccab", "4938", "8f97", "3327", "8029", "41f2", "a04f", "c7f9", "b453", "90a5", "25dc", "26b0", "cb42", "de89", "2451", "1dd3", "7f2c", "8919", "f3a9", "b88f", "eaa8", "776a", "6236", "98f5", "492b", "507d", "18e8", "cfb5", "76fd", "6017", "30de", "bbae", "354e", "4013", "3153", "e9cc", "cba9", "25ea", "c06c", "a166", "faf1", "2264", "2179", "cf30", "4b47", "3446", "b213", "88a3", "6253", "db88", "c38c", "a48c", "3e4f", "7208", "9dcb", "fc77", "e2cf", "8552", "f6f8", "7079", "42ef", "391e", "8a6d", "2154", "d964", "49ec"]
    
    for user_pw in pos_pw_list:
        user_pw_hash = hash_pw(user_pw)

        if user_pw_hash == correct_pw_hash:
            print("Correct password:", user_pw)
            print("Welcome back... your flag, user:")

            decryption = str_xor(flag_enc.decode(), user_pw)
            print(decryption)
            return

    print("No matching password found.")
```
That looks like a lot, but the only difference between this function and the last one is the `pos_pw_list` being the updated one.

Running that new script, we get the final flag `academy{fl45h_5pr1ng1ng_f8cf5d9c}`

# PW Crack 5
PW Crack 5 adds an entire dictionary.txt file in that has the password list. Way too much to do manually now, if for some reason you chose to do it manually before. 

So, let's take a look at the original code and work from there:
```
import hashlib

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

flag_enc = open('level5.flag.txt.enc', 'rb').read()
correct_pw_hash = open('level5.hash.bin', 'rb').read()


def hash_pw(pw_str):
    pw_bytes = bytearray()
    pw_bytes.extend(pw_str.encode())
    m = hashlib.md5()
    m.update(pw_bytes)
    return m.digest()


def level_5_pw_check():
    user_pw = input("Please enter correct password for flag: ")
    user_pw_hash = hash_pw(user_pw)
    
    if( user_pw_hash == correct_pw_hash ):
        print("Welcome back... your flag, user:")
        decryption = str_xor(flag_enc.decode(), user_pw)
        print(decryption)
        return
    print("That password is incorrect")



level_5_pw_check()
```
Very similar to before, but as expected it is using the password list and comparing it to hashes. The only important part is that `def level_5_pw_check()` function. 

We'd want to change as little as possible from this function, so we essentially want to just make it read the dictionary file and I'll have it load that into a list to be used the same way the previous CTFs did.
```
def level_5_pw_check():
    pos_pw_list = []
    with open("dictionary.txt", "r", encoding="utf-8") as file:
        for line in file:
                cleanline = line.rstrip("\n")
                pos_pw_list.append(cleanline)

        for user_pw in pos_pw_list:
            user_pw_hash = hash_pw(user_pw)

            if user_pw_hash == correct_pw_hash:
                print("Correct password:", user_pw)
                print("Welcome back... your flag, user:")

                decryption = str_xor(flag_enc.decode(), user_pw)
                print(decryption)
                return
```
Let's break it down a little bit more. The `pos_pw_list = []` just creates an empty list that can be used for the function. As we add things to that list, it will be filled in, but it will all remain "in memory" meaning every time the code executes it will have to reload the list from the .txt file.

That `with open...` function essentially loads the `dictionary.txt` file in and takes line by line, loading each one into the `pos_pw_list` list we made before. Pretty straightforward.

Then, the `for user_pw in pos_pw_list` loop is exactly the same as before, loading each item from that `pos_pw_list` and trying them as passwords.

So then the complete file would become:
```
import hashlib

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

flag_enc = open('level5.flag.txt.enc', 'rb').read()
correct_pw_hash = open('level5.hash.bin', 'rb').read()


def hash_pw(pw_str):
    pw_bytes = bytearray()
    pw_bytes.extend(pw_str.encode())
    m = hashlib.md5()
    m.update(pw_bytes)
    return m.digest()


def level_5_pw_check():
    pos_pw_list = []
    with open("dictionary.txt", "r", encoding="utf-8") as file:
        for line in file:
                cleanline = line.rstrip("\n")
                pos_pw_list.append(cleanline)

        for user_pw in pos_pw_list:
            user_pw_hash = hash_pw(user_pw)

            if user_pw_hash == correct_pw_hash:
                print("Correct password:", user_pw)
                print("Welcome back... your flag, user:")

                decryption = str_xor(flag_enc.decode(), user_pw)
                print(decryption)
                return



level_5_pw_check()
```
Which gives you the final flag `academy{h45h_sl1ng1ng_27d64792}`
