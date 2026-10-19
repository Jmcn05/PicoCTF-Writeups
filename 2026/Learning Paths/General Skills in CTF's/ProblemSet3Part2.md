# Problem Set 3 (Part 2)

# Static Ain't Always Noise
A multistep problem using a prewritten script.

The program provides two files to the user, `static` and `ltdis.sh`. First, take a look at both files.

Using `cat` on static makes it appear as a bunch of random noise, not even worth trying to piece together. Interestingly, one of the things that didn't appear as noise in this file when I ran `cat` was the actual flag, but for the sake of doing it properly I continued on.

Using `cat` on `ltdis.sh` shows a bash script that you can tell takes an input from a file and then provides a decrypted output. So naturally, I ran `./ltdis.sh static`.

This provided two files, `static.ltdis.strings.txt` and `static.ltdis.x86_64.txt`. Using `cat` on `static.ltdis.strings.txt` provides the output:
```
    318 /lib64/ld-linux-x86-64.so.2
    481 puts
    486 __libc_start_main
    498 __cxa_finalize
    4a7 libc.so.6
    4b1 GLIBC_2.2.5
    4bd GLIBC_2.34
    4c8 _ITM_deregisterTMCloneTable
    4e4 __gmon_start__
    4f3 _ITM_registerTMCloneTable
   1071 PTE1
   110b u+UH
   2008 Oh hai! Wait what? A flag? Yes, it's around here somewhere!
   20c7 9*3$"
   3020 academy{d15a5m_t34s3r_fac3431a}
   3040 GCC: (Ubuntu 13.3.0-6ubuntu2~24.04.1) 13.3.0
   33e9 Scrt1.o
   33f1 __abi_tag
   33fb crtstuff.c
   3406 deregister_tm_clones
   341b __do_global_dtors_aux
   3431 completed.0
   343d __do_global_dtors_aux_fini_array_entry
   3464 frame_dummy
   3470 __frame_dummy_init_array_entry
   348f static.c
   3498 __FRAME_END__
   34a6 _DYNAMIC
   34af __GNU_EH_FRAME_HDR
   34c2 _GLOBAL_OFFSET_TABLE_
   34d8 __libc_start_main@GLIBC_2.34
   34f5 _ITM_deregisterTMCloneTable
   3511 puts@GLIBC_2.2.5
   3522 _edata
   3529 _fini
   352f __data_start
   353c __gmon_start__
   354b __dso_handle
   3558 _IO_stdin_used
   3567 _end
   356c __bss_start
   3578 main
   357d __TMC_END__
   3589 _ITM_registerTMCloneTable
   35a3 flag
   35a8 __cxa_finalize@GLIBC_2.2.5
   35c3 _init
   35ca .symtab
   35d2 .strtab
   35da .shstrtab
   35e4 .interp
   35ec .note.gnu.property
   35ff .note.gnu.build-id
   3612 .note.ABI-tag
   3620 .gnu.hash
   362a .dynsym
   3632 .dynstr
   363a .gnu.version
   3647 .gnu.version_r
   3656 .rela.dyn
   3660 .rela.plt
   366a .init
   3670 .plt.got
   3679 .plt.sec
   3682 .text
   3688 .fini
   368e .rodata
   3696 .eh_frame_hdr
   36a4 .eh_frame
   36ae .init_array
   36ba .fini_array
   36c6 .dynamic
   36cf .data
   36d5 .bss
   36da .comment
```

So the final flag which appears inside of that text is `academy{d15a5m_t34s3r_fac3431a}`.


# strings it
strings it was one of the few that took me a bit of time to figure out. My initial instinct was to use `cat strings | grep "academy" ` to find it, but that didn't work.

That returned `grep: (standard input): binary file matches` and there was no flags that worked properly that I could find to solve the challenge without printing the entire file.

So back to square one, I attempted to then use the `strings` command. Combined with `grep`, it found the flag. So `strings strings | grep "academy"` returned the flag `academy{5tRIng5_1T_d47eAaCB}`


# plumbing
While this is incredibly important to know, it's also incredibly easy to do. 

The instructions say to connect using `xebec.cylabacademy.net 15462`, so using that instructions simply type `nc xebec.cylabacademy.net 15462`.

That provides a huge output, 
```
...
Again, I really don't think this is a flag
This is defintely not a flag
This is defintely not a flag
Again, I really don't think this is a flag
I don't think this is a flag either
Not a flag either
I don't think this is a flag either
This is defintely not a flag
Not a flag either
I don't think this is a flag either
Not a flag either
This is defintely not a flag
This is defintely not a flag
I don't think this is a flag either
Not a flag either
Not a flag either
Again, I really don't think this is a flag
This is defintely not a flag
Not a flag either
Again, I really don't think this is a flag
I don't think this is a flag either
Not a flag either
I don't think this is a flag either
Not a flag either
Not a flag either
Not a flag either
This is defintely not a flag
Again, I really don't think this is a flag
This is defintely not a flag
Again, I really don't think this is a flag
Not a flag either
Again, I really don't think this is a flag
This is defintely not a flag
This is defintely not a flag
Not a flag either
Not a flag either
This is defintely not a flag
This is defintely not a flag
Not a flag either
Not a flag either
Not a flag either
Not a flag either
Not a flag either
Again, I really don't think this is a flag
I don't think this is a flag either
Not a flag either
Not a flag either
Not a flag either
Again, I really don't think this is a flag
This is defintely not a flag
Not a flag either
Not a flag either
Not a flag either
Again, I really don't think this is a flag
This is defintely not a flag
Not a flag either
Not a flag either
This is defintely not a flag
I don't think this is a flag either
Not a flag either
Again, I really don't think this is a flag
I don't think this is a flag either
Not a flag either
This is defintely not a flag
Not a flag either
Not a flag either
Not a flag either
Again, I really don't think this is a flag
This is defintely not a flag
This is defintely not a flag
I don't think this is a flag either
This is defintely not a flag
Not a flag either
...
```
I won't put the whole thing in but you understand the point.

So, similar to all the other times we've had a giant string we needed to find something, just use `grep`. 

`nc xebec.cylabacademy.net 13195 | grep academy` provides the final flag `academy{digital_plumb3r_CB83CD6b}`.