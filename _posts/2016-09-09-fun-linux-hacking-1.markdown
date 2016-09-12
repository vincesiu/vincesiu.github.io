---
layout: post
title:  "Fun Linux Hacking 1: Figuring out 32-bit vs 64-bit limitations for my cpu and memory"
categories: linux
---

### Disclaimer:

Take my statements here with a grain of salt, I am but a humble student who is trying his best to learn about this topic. Feel free to pm me with any improvements/corrections!

--------------

### Introduction

One of the things that I have been doing recently in my spare time is retrofitting an old computer to function as a linux server for me to play on at school. It is an old HP computer that was brough ten years ago, it was running Windows Vista 32 bit (What!!! 32 bit!?!?! I haven't seen a 32 bit machine in... forever!), and I wanted to install Arch Linux on it.

The focus of this post will be looking at looking at 32 bit vs 64 bit things, deciding if my cpu is compatible to run a 64 bit operating system, and determining how much memory I can add.

-------------

### 32 bit vs 64 bit

There are two big differences between 32 bit and 64 bit:
    1. Differences in word sizes (A word is the smallest unit on which a CPU operates on)
    2. Differences in size of total memory that can be supported (4 gigabytes for 32 bit, 16 exbibytes for 64 bit)

Unfortunately, not everything is so clear cut between these two. There are ways for 32 bit machines to be able to access more than 4 gigabytes of memory, and there are ways to run 32 bit applications on 64 bit cpus. For me, when I was starting to dive into this, I was very confused at first about what can support what, but I think I broke it down into the following:

    1. CPU (physical hardware)
    2. Operating System
    3. Application

Each of these can be split up into 32 bit or 64 bit versions, and the thing is it can get very complicated mixing and matching, since there are lot of edge cases to consider. For example, you can run a 32 bit operating system on a 64 bit cpu. I reccomend researching more into it, but be careful; the rabbit hole is very deep.

---------------

### CPU compatiblity

You can check directly if your cpu can handle a 64 bit process by running the command, and checking if the "lm" flag is enabled. Here is a sample output from my computer:

```
> grep flags /proc/cpuinfo

flags           : fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush dts acpi mmx fxsr sse sse2 ss ht tm pbe syscall nx lm constant_tsc arch_perfmon pebs bts rep_good nopl aperfmperf eagerfpu pni dtes64 monitor ds_cpl est tm2 ssse3 cx16 xtpr pdcm lahf_lm dtherm
```

This command will give you a ton of juicy information about your processor, but the main one which we are interested in is the "lm" flag, or "long mode" flag. The presence of this flag means that our processor can support a 64 bit operating system. [^2]

If the "lm" flag is present, it means that regular 32-bit registers are extended to 64 bit (eg. eax to rax), and some extra registers are added as well. [^3]

This means that my current processor can run a 64 bit OS! Sweet! Looks like 64-bit Arch Linux is going in!!!

--------------

### Finding out more information about your system

One of the tools that I found to find out more about my system through the command line (ie I'm too lazy to google the model of my computer to find the default equipment inside) is dmidecode, which is a tool which dumps information about the system's hardware components. Digging around in the man pages, I found that it categorizes hardware into different types, and the following were the most interesting:

- type 2: baseboard
: this is the motherboard, and is pretty important for finding out which connections are available

- type 4: processor
: this is the cpu, and you can find out a LOT of juicy details about it with this command

- type 5: memory controller
: this is the component which dictates the maximimum amount of RAM supported, and the number of slots

- type 6: memory module
: this shows basic details about individual cards which are attached. There will most likely be multiple entries which show up. If you want specific information about each memory module, look at type 17, memory device.


Running just the `dmidecode` command will get you a massive dump of information, so I prefer to view things one type at a time. For example, if I wanted to see information about the baseboard, I would run `dmidecode --type 2`.

---------------

### Checking how much memory I can add to my system

So! Looks like I have a 64 bit CPU on my computer! But can I add more than 4 gigabytes of RAM? Let's turn to dmidecode! We're interested in the memory controller, so --type 5.

Output comes out to be:

```
 > sudo dmidecode --type 5
[sudo] password for vince:
# dmidecode 3.0
Getting SMBIOS data from sysfs.
SMBIOS 2.4 present.

Handle 0x0005, DMI type 5, 24 bytes
Memory Controller Information
        Error Detecting Method: 8-bit Parity
        Error Correcting Capabilities:
                None
        Supported Interleave: One-way Interleave
        Current Interleave: One-way Interleave
        Maximum Memory Module Size: 1024 MB
        Maximum Total Memory Size: 4096 MB
        Supported Speeds:
                Other
        Supported Memory Types:
                Other
        Memory Module Voltage: 5.0 V
        Associated Memory Slots: 4
                0x0006
                0x0007
                0x0008
                0x0009
        Enabled Error Correcting Capabilities:
                None
```

Darn! It looks like the maximum memory I can have is 4 gigs, and each memory module can have a maximum of 1 gig each. 

Anyways, moving on. Even if your computer has a 32 bit processor, you shouldn't always give up hope! Some 32 bit computers can use more than 4 gigabytes of ram surprisingly. There is something called PAE, or Physically Addressed Memory, which involved increasing the number of address lines so that there would be a higher physical address space, but software would still be limited to the 32 bit virtual address space. So, armed with this knowledge, go check out your memory module! What's the max amount of memory your computer can handle? [^4]

Interleaved memory is fascinating, and using it can allow for faster word accesses by splitting up the bits in words across different units of memory. This technique is used in some of the higher levels of RAID as well to allow for increased memory IO throughput. [^5]


------------

### Extra Resources

- [https://superuser.com/questions/9083/can-a-32-bit-os-run-in-a-64-bit-processor](https://superuser.com/questions/9083/can-a-32-bit-os-run-in-a-64-bit-processor)
- [https://en.wikipedia.org/wiki/Memory_bank](https://en.wikipedia.org/wiki/Memory_bank)

----

### References

[^2]: [https://unix.stackexchange.com/questions/43539/what-do-the-flags-in-proc-cpuinfo-mean](https://unix.stackexchange.com/questions/43539/what-do-the-flags-in-proc-cpuinfo-mean)
[^3]: [http://wiki.osdev.org/X86-64](http://wiki.osdev.org/X86-64)
[^4]: [https://en.wikipedia.org/wiki/Physical_Address_Extension](https://en.wikipedia.org/wiki/Physical_Address_Extension)
[^5]: [https://en.wikipedia.org/wiki/Interleaved_memory](https://en.wikipedia.org/wiki/Interleaved_memory)
