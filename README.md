# uJ

Fully functional, efficient JVM for 8bit AVR and friends. This was made by [Dmitry Grinberg](http://dmitry.gr/index.php?r=05.Projects&proj=12.%20uJ%20-%20a%20micro%20JVM).

#### What?

uJ is a Java VM for microcontrollers. It implements the entirety of the java bytecode and is written entirely in C, so that it may run on any processor. It has been tested and found functional on 8-bit AVR devices (ATmega64, Atmega128), some Microchip 16-bit PIC devices (dsPIC33FJ128GP802, dsPIC33FJ64GP802, PIC24FJ32GA002), and a few other architectures. It is quite efficient, fast, and usable for actual real-life situations. Minimum requirements? A few dozen K of code space and a few hundred bytes of RAM is all you need to get started. More is better, as always.

#### Why?

Lots of people want to program microcontrollers, few understand memory management, peripherals, and C in general. Several crutches exist for this (PICAXE, Arduino, etc), none of which really address the problem that many people still have no idea how to use pointers and other C-level code, but still want performance and ease of programming. Java is very well known, and most people studying in universities today learn just it (sad but true). So I set out to make a fully working JVM for a microcontroller. The goals were simple: complete support of the java bytecode, including exceptions, inheritance, interfaces, synchronization, threading, garbage collection, arrays (including multi-dimensional ones), etc...

#### How?

There were a few interesting challenges in the project, such as fitting into the code and data memory limits, reasonableness of speed, and in general the design. The VM is very modular, wherein various pieces can be disabled or enabled to tune the VM features and size. One of the major design guidelines was not copying class files to RAM. This would allow devices with very little RAM to still run the JVM. Java class files, however, are very unpleasant to parse, since for all effective purposes they are sequential-access only. All data structures are variable length, so to get to the N-th method, you have to read lots of file pieces before then (skiping all constants, previous methods, etc...). Some ways of speeding this up exist and are used by the VM, but a better method would be a better container format. uJ supports this better container format: UJC.

## Implementation Details

[See here.](http://web.archive.org/save/http://dmitry.gr/index.php?r=05.Projects&proj=12.%20uJ%20-%20a%20micro%20JVM)
