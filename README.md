# DotNet_CCEE

# .NET Framework
1. Software development platform hai jo Microsoft ne banaya
2. Multiple programming languages support karta hai (C#, VB.NET, F#, etc.)
3. Windows applications, web applications, services banane ke liye use hota hai

## Main Components:

CLR (Common Language Runtime) - Execution engine
FCL (Framework Class Library) - Pre-built classes ka collection
Language Compilers - C#, VB.NET compilers

##  Intermediate Language (IL)
CPU-independent code hai
Jab tum C# ya VB.NET code likhte ho, wo directly machine code mein convert nahi hota
Pehle MSIL (Microsoft Intermediate Language) mein convert hota hai
IL ko bytecode bhi kehte hain

* Source Code (.cs) → Compiler → IL Code (.exe/.dll) → JIT Compiler → Native Machine Code

  MCQ Focus:

IL ko MSIL ya CIL (Common IL) bhi bolte hain
.exe/.dll files actually IL code contain karti hain
JIT compiler IL ko machine code mein convert karta hai runtime pe
