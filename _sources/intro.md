# Introduction

Welcome to a short primer on using the C & C++ programming languages. These notes were written for students on the ACSE and EDSML Masters courses in the Earth Science & Engineering Department at Imperial College London.

These notes assume some previous programming experience in Python, equivalent to that of the Modern Programming Methods or Numerical Programming in Python courses, however they should be possible for anyone with previous experience coding in an interpretted language.

This primer combines some notes introducing C-like languages to novice users, along with some exercises to practise your new knowledge. It is split into three sections,  It will probably take a maximum of 16 hours to work through, depending on your previous knowledge and how far you go with the exercises.

## Why do we teach C++?

Python code is relatively easy to run (although not always easy to write), but doesn't always run very quickly. By using a compiled language like C++ we can get "closer to the metal" of the computer processor and write code which generates a solution much faster (sometimes hundreds or thousands of times faster). Often this performance difference doesn't matter, and the time taken to develop & maintain the code is more important, but for certain large scale calculations, which can take hours or days to run, then these differences become important.

There are many other compiled languages in existence (eg. Fortran, Java, C#, ...) but C and C++ are currently some of the most widely used, and in demand. Unlike niche scientific languages such as Fortran, they are used both for numerical and systems programming and many modern machine learning frameworks have a C or C++ interface.

## How does C/C++ differ from Python?

Python is what is known as an interpreted language. To run code, you point a single program, the interpreter, at your source file, and it translates and runs the instructions in a way your computer can understand. C & C++ are compiled languages. A tool called a compiler is used to convert your human-readable source files into an executable instruction file your machine understands. This file can then be run many times.

Python is also a garbage-collected language. It cleans up (eventually) all the memory you use to hold variables in your programs, once it realises you're no longer interested in them. C-like languages give you, as a programmer, more power & control on where in your computer memory things live, and how long they stay around for. In return, it is often the programmer's job to clean up once you have finished

## Summary

In this section we have introduced the C & C++ programming languages, and given a brief motivation for why we might want to use them in preference to another language such as Python.

In the next section we will look at how to compile and run C & C++ code on your own computer.

