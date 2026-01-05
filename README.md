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

1. IL ko MSIL ya CIL (Common IL) bhi bolte hain
2. .exe/.dll files actually IL code contain karti hain
3. JIT compiler IL ko machine code mein convert karta hai runtime pe

## 3. Assemblies (EXE & DLL)
Assembly kya hai?

1. .NET application ki fundamental unit hai
2. Deployment, versioning, security ka basic unit
3. IL code + metadata + resources contain karta hai
   
Types:
A) EXE (Executable Assembly)

Entry point hota hai (Main method).
Directly execute ho sakta hai.
Process Assembly bhi kehte hain.
Example: Console application, Windows application.

B) DLL (Dynamic Link Library)

No entry point (Main method nahi hota).
Cannot execute directly.
Dusre applications ke liye reusable code provide karta hai.
Example: Class libraries, shared code.

```
MCQ Focus Points:

EXE has entry point, DLL doesn't
Manifest is compulsory in every assembly
GAC location: C:\Windows\Assembly
gacutil.exe tool GAC mein assembly install karne ke liye
Strong name = cryptographic signature for uniqueness
```
