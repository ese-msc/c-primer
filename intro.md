# Introduction

Welcome to a short primer on using the C & C++ programming languages. These notes were written for students on the ACSE and EDSML Masters courses in the Earth Science & Engineering Department at Imperial College London.

The notes assume some limited previous programming experience in Python, equivalent to that of the Modern Programming Methods course.

This primer combines some notes introducing C-like languages to novice users, along with some exercises to practise your new knowledge. It will probably take a maximum of X hours to work through.

## Why do we teach C++?

Python code is relatively easy to run (although not always easy to write), but doesn't always run very quickly. By using a compiled language like C++ we can get "closer to the metal" of the computer and write code which generates a solution much sooner.

## How does C/C++ differ from Python?

Python is what is known as an interpretted language. To run code, you point a single program, the interpreter at your source file, and it translates and runs the instructions in a way your computer can understand. C & C++ are compiled languages. A tool called a compiler is used to convert your human-readable source files into an executable instruction file your machine understands. This file can then be run many times.

Python is also a garbage-collected language. It cleans up (eventually) all the memory you use in your programs, once it realises you're no longer interested in it. C-like languages give you, as a programmer, more control on where in your computer memory things live, and how long they stay around for. In return, it is often the programmer's job to clean up.

## Running C/C++ programs

### Web based solutions

- replit.com


### Windows: Visual Studio

For Windows users only, you can obtain the Microsoft C/C++ compiler by downloading the Visual Studio community package [here](). Visual Studio is a sister package to Visual Studio Code, which combines build tools for several programming languages with an Integrating Development Environment (IDE) to code them in.

### Apple macs: Using gcc & VS code