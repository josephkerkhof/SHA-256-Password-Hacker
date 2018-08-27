# SHA-256 Password Hacker

## Summary of the Problem

Given a byte array hashed with SHA-256 encryption, brute force check all possible password combinations to discover the un-hashed password.

## Purpose of the Problem

This supplemental project in my Data Structures (CS 271) course was given to illustrate how poor brute force algorithms are in solving problems. In this case however, it is the only solution. At the time of my solution **no other Computer Science student at UW-Oshkosh had discovered a way to crack the password**.

## Problem Details

### What I Was Given

- The password is 8 characters long
- The password is made up of any of the following character combinations
  - Uppercase letters (A-Z)
  - Lowercase letters (a-z)
  - Numbers (0-9)

### The Math

Since it is known that there are 8 digits to the password and 62 different combinations for each digit (26 uppercase letters + 26 lowercase letters + 10 digits) there are 8^62 different total password combinations equating to a total of
_~98 septendecillion_ or 98,079,714,615,416,886,934,934,209,737,619,787,751,599,303,819,750,539,264 to be precise.

## How I Solved This Problem

### The Time Constraint

After doing some rough estimations, having a single threaded process brute force thru 98 septendecillion combination would take roughly _5.5 years_ to get to the last possible combination. This would obviously work, but take far too long since I was bound by a semester due date. I needed a way to speed things up.

### Splitting the Problem into Chunks

Instead of having one thread check all possibilities, I could solve the problem with many threads each checking a separate portion of the brute force. When I was solving this problem, our Computer Science Linux lab had 32 computers each with a quad-core processor. I decided to split the problem into 124 chunks utilizing 31 computers each running 4 threads - one for each processor. Using this method I reduced the runtime of the entire process from 5.5 years to **just over 2 weeks**, much more doable in a semester's worth of time.

### The PasswordHacker.java file

When compiled and run, this program writes 124 different Java programs to a separate file. There are 4 in a group - each for a different machine. Each group also gets a separate shell script written to make starting the threads on each machine easier.

### Executing the Solution

Each day I would SSH into each Linux Lab computer and ensure the process was running with a [nice value of 19](https://en.wikipedia.org/wiki/Nice_%28Unix%29).
