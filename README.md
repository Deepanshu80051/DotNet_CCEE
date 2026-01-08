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

```
Sample MCQs:
Q: Assembly ka metadata kaha store hota hai?

a) IL Code
b) Manifest ✓
c) Resources
d) GAC

Q: Shared assembly kaha install hoti hai?

a) Application folder
b) System32
c) GAC ✓
d) Temp folder

Q: Strong name mein kya include hota hai?

a) Only assembly name
b) Name + Version
c) Name + Version + Culture + Public Key ✓
d) Only public key
```
##  Common Language Runtime (CLR)

CLR kya hai?

1. .NET Framework ka heart hai
2. Virtual machine jaisa kaam karta hai
3. IL code ko execute karta hai
4. Managed execution environment provide karta hai
```
Source Code
    ↓
Language Compiler
    ↓
IL Code + Metadata (Assembly)
    ↓
CLR Components:
├── Class Loader
├── JIT Compiler
├── Garbage Collector
├── Security Manager
├── Exception Manager
└── Thread Manager
    ↓
Native Machine Code
    ↓
Execution
```
1. JIT compiler CLR ka part hai
2. Type safety verification CLR karta hai


## JIT Compilation (Just-In-Time)
1. IL code ko native machine code mein convert karta hai
2. Runtime pe (execution time pe) compilation hota hai

   ### types
   3- normal(default), pre-jit(ahead of time) , econo-jit

MCQ Focus:

1. 3 types of JIT: Normal, Pre-JIT, Econo-JIT
2. ngen.exe pre-JIT ke liye use hota hai
3. First call pe compilation, subsequent calls cached code use karti hain
4. JIT IL ko machine code mein convert karta hai

Q: Agar ek method ko 10 baar call kiya jaye, to JIT compilation kitni baar hoga?

a) 10 baar
b) 1 baar ✓
c) 0 baar
d) 5 baar

void MyMethod() {
    int x = 10;      // Stack pe
    double y = 5.5;  // Stack pe
}  // Method end = x, y automatically removed
```

#### 2. **Heap Memory**
- **Reference types** (class, array, string, delegate) store hote hain
- **Dynamic allocation**
- **Garbage Collector** manage karta hai
- **Slower than stack**
- **Larger size** available

### Heap Organization (Generational GC):

**Generation 0 (Gen 0):**
- **Newly created objects**
- **Fastest GC**
- **Frequently collected**
- Most objects **die young** (short-lived)

**Generation 1 (Gen 1):**
- Objects jo **Gen 0 collection survive** kar gaye
- **Medium-term objects**
- **Buffer zone**

**Generation 2 (Gen 2):**
- **Long-lived objects**
- Collections **rare and expensive**
- Static members, application-level objects

**Large Object Heap (LOH):**
- Objects **> 85,000 bytes**
- **Directly Gen 2** mein allocate hote hain
- Arrays, large collections

### Memory Allocation Process:
```
Object Creation Request
    ↓
CLR checks available space
    ↓
If space available:
    - Allocate on heap
    - Initialize object
    - Return reference
    ↓
If space NOT available:
    - Trigger Garbage Collection
    - Compact heap
    - Retry allocation
```

### Stack vs Heap Comparison:

| Feature | Stack | Heap |
|---------|-------|------|
| **Stores** | Value types | Reference types |
| **Speed** | Fast | Slower |
| **Size** | Limited (~1MB) | Large |
| **Lifetime** | Scope-based | GC-managed |
| **Allocation** | Automatic | Manual (new) |
| **Cleanup** | Automatic | GC |

### MCQ Focus:
- **Value types → Stack, Reference types → Heap**
- **3 Generations** + LOH
- Stack = **LIFO**, automatic cleanup
- Heap = **GC** managed
- **LOH threshold = 85,000 bytes**

**Sample MCQs:**

Q: Value types kaha store hote hain?
- a) Heap
- b) Stack ✓
- c) GAC
- d) Cache

Q: Heap memory ko kaun manage karta hai?
- a) Programmer
- b) Stack
- c) Garbage Collector ✓
- d) Operating System

Q: Kitne generations hain GC mein?
- a) 2
- b) 3 ✓
- c) 4
- d) 5

Q: Large Object Heap kis size se shuru hota hai?
- a) 10,000 bytes
- b) 50,000 bytes
- c) 85,000 bytes ✓
- d) 100,000 bytes

---

## 7. Garbage Collection (GC)

### Garbage Collector kya hai?
- **Automatic memory management** system
- **Unused objects** ko identify aur remove karta hai
- **Memory leaks prevent** karta hai
- **Background thread** mein run hota hai

```
**Sample MCQs:**

Q: GC ke kitne phases hain?
- a) 2
- b) 3 ✓
- c) 4
- d) 5

Q: Unmanaged resources cleanup ke liye kaun sa interface use hota hai?
- a) IComparable
- b) IDisposable ✓
- c) IEnumerable
- d) ICloneable

Q: Server GC kis application ke liye better hai?
- a) Desktop apps
- b) Mobile apps
- c) Web applications ✓
- d) Console apps

Q: GC.Collect() method ko kab use karna chahiye?
- a) Har object create karne ke baad
- b) Method ke end mein
- c) Generally avoid karna chahiye ✓
- d) Har loop mein

Q: Finalizer ka syntax kya hai?
- a) finalize()
- b) ~ClassName() ✓
- c) Dispose()
- d) Cleanup()

**Sample MCQs:**

Q: AppDomain kya provide karta hai?
- a) Process isolation
- b) Logical isolation ✓
- c) Thread isolation
- d) Memory isolation only

Q: AppDomain ko unload karna possible hai?
- a) Yes ✓
- b) No
- c) Only in debug mode
- d) Only with admin rights

Q: Har .NET application mein kitne AppDomains minimum hote hain?
- a) 0
- b) 1 ✓
- c) 2
- d) 3

Q: Cross-AppDomain communication ke kitne tarike hain?
- a) 1
- b) 2 ✓
- c) 3
- d) 4

Q: Marshal by Value mein kya hota hai?
- a) Object ka reference pass hota hai
- b) Object ka copy pass hota hai ✓
- c) Object delete ho jata hai
- d) Object shared hota hai

---
## Common Type System (CTS)

- **.NET Framework ka type system**
- **Type safety** ensure karta hai
-  C# ka `int` = VB.NET ka `Integer` = **same type** (System.Int32)


Built-in Types (System Namespace):
├── Integer Types
│   ├── sbyte  (System.SByte)    - 8 bit signed
│   ├── byte   (System.Byte)     - 8 bit unsigned
│   ├── short  (System.Int16)    - 16 bit signed
│   ├── ushort (System.UInt16)   - 16 bit unsigned
│   ├── int    (System.Int32)    - 32 bit signed
│   ├── uint   (System.UInt32)   - 32 bit unsigned
│   ├── long   (System.Int64)    - 64 bit signed
│   └── ulong  (System.UInt64)   - 64 bit unsigned
│
├── Floating Point Types
│   ├── float   (System.Single)  - 32 bit
│   ├── double  (System.Double)  - 64 bit
│   └── decimal (System.Decimal) - 128 bit (financial)
│
├── Other Types
│   ├── bool    (System.Boolean) - true/false
│   └── char    (System.Char)    - 16 bit Unicode

User-Defined Value Types
 1. Structures(struct)
 2. Enumerations (enum)


### CTS Type Hierarchy:
```
System.Object (Root of all types)
│
├── Value Types (System.ValueType)
│   ├── Primitive Types (int, float, bool, etc.)
│   ├── Structures (struct)
│   └── Enumerations (enum)
│
└── Reference Types
    ├── Classes (class)
    ├── Interfaces (interface)
    ├── Delegates (delegate)
    ├── Arrays
    └── Strings
```

* -> Conversion Methods
 ```
  string s = "123";
int i = Convert.ToInt32(s);
int j = int.Parse(s);
int.TryParse(s, out int k);  // Safe parsing
```

CTS Rules: Common Type System

1. Every type derives from System.Object
2. Value types cannot be null (unless Nullable<T>)
3. Value types are sealed (no inheritance)
4. Type safety enforced by CLR
5. CLS compliance for interoperability

Q: Value types kisse inherit karte hain?

a) System.Object
b) System.ValueType ✓
c) System.Type
d) System.Value

Q: Boxing kya hai?

a) Reference to value conversion
b) Value to reference conversion ✓
c) Type casting
d) Memory allocation

Q: Unboxing ke liye kya required hai?

a) Implicit cast
b) Explicit cast ✓
c) No cast needed
d) Automatic conversion

Q: System.Object kis type ka base hai?

a) Only value types
b) Only reference types
c) All types ✓
d) Only classes

## Common Language Specification (CLS)
1. Subset of CTS hai

CTS (Complete Type System)
│
└── CLS (Common Subset for Interoperability)

### MCQ Focus:
- **CLS = subset of CTS**
- **Interoperability** ka purpose
- **Unsigned types** not CLS-compliant
- **Public members** must be compliant
- **[CLSCompliant]** attribute
- **Case-insensitive** naming
- Alternative methods for **operator overloading**

**Sample MCQs:**

Q: CLS ka purpose kya hai?
- a) Type safety
- b) Memory management
- c) Language interoperability ✓
- d) Security

Q: CLS, CTS ka kya hai?
- a) Superset
- b) Subset ✓
- c) Same thing
- d) Opposite

Q: Kaun sa type CLS-compliant NAHI hai?
- a) int
- b) uint ✓
- c) string
- d) bool

Q: CLS compliance check karne ke liye kaun sa attribute use hota hai?
- a) [CLS]
- b) [CLSCompliant] ✓
- c) [Compliant]
- d) [CLSCheck]

Q: CLS-compliant code mein naming ka kya rule hai?
- a) Case-sensitive
- b) Case-insensitive ✓
- c) Only lowercase
- d) Only uppercase

Q: Agar library VB.NET aur C# dono se use honi hai, to kya use karna chahiye?
- a) CTS
- b) CLS ✓
- c) CLR
- d) JIT

---


Symmetric (same key) vs Asymmetric (public/private) encryption

* Sample MCQs:
  
Q: CAS ka full form kya hai?

a) Common Access Security
b) Code Access Security ✓
c) Central Access System
d) Code Authentication Security

Q: Role-based security kis pe based hai?

a) Code origin
b) User identity ✓
c) Assembly name
d) File location

Q: Kaun sa security zone sabse zyada trusted hai?

a) Internet
b) Intranet
c) My Computer ✓
d) Trusted Sites

Q: SecurityAction.Demand kya karta hai?

a) Grants permission
b) Checks if caller has permission ✓
c) Denies permission
d) Removes permission

Q: SHA256 kis type ka algorithm hai?

a) Encryption
b) Hashing ✓
c) Compression
d) Digital signature

# CDAC CCEE Exam - Important Points Summary
Must Remember for MCQs:
.NET Framework:

CLR = execution engine
IL = intermediate code
JIT = runtime compilation (3 types)
FCL = class library

Assemblies:

EXE = entry point, DLL = no entry point
Manifest = assembly metadata
GAC = shared assemblies
Strong name = unique identity

Memory:

Stack = value types, LIFO, automatic
Heap = reference types, GC managed
3 Generations (0, 1, 2) + LOH (>85KB)

Types:

CTS = complete type system
CLS = interoperability subset
Boxing = value → reference (slow)
Value types inherit from System.ValueType

GC:

3 phases: Marking, Compacting, Cleanup
IDisposable for unmanaged resources
Avoid GC.Collect() calls
Finalizer = destructor (~ClassName)

Security:

CAS = code-based permissions
Role-based = user/role permissions
Symmetric = same key
Asymmetric = public/private keys
SHA256 = hashing (one-way)

#Practice MCQ Set:
Q1: .NET code kis form mein compile hota hai?
a) Machine code  b) IL code ✓  c) Assembly  d) Bytecode
Q2: Private assembly kaha store hoti hai?
a) GAC  b) Application folder ✓  c) System32  d) Temp
Q3: Value types ka default value kya hai?
a) null  b) 0 (or equivalent) ✓  c) undefined  d) error
Q4: Gen 0 collection ki frequency kya hai?
a) Rare  b) Medium  c) Frequent ✓  d) Never
Q5: CLS-compliant nahi hai:
a) int  b) uint ✓  c) string  d) bool
Q6: AppDomain unload possible hai?
a) Yes ✓  b) No  c) Only in debug  d) Admin only
Q7: JIT ki full form:
a) Just In Time ✓  b) Join In Thread  c) Jump In Type  d) Java Interface Type
Q8: Boxing kis type ki conversion hai?
a) int to long  b) value to reference ✓  c) string to int  d) class to interface
Q9: Security zone with minimum trust:
a) MyComputer  b) Intranet  c) Internet  d) Untrusted ✓
Q10: Garbage Collector kab run hota hai?
a) Manually only  b) After every method  c) When memory needed ✓  d) Never


🔁 Quick Revision Points – CDAC CCEE (.NET Framework)
🔢 Must Remember Numbers

-3 Generations in Garbage Collector (Gen 0, Gen 1, Gen 2)

-85,000 bytes → Large Object Heap (LOH) threshold

-1 Default AppDomain (minimum per process)

-1.0.0.0 → Assembly version format

-2 Types of assemblies
EXE
DLL

-2 Cross-AppDomain communication methods
Marshal by Value
Marshal by Reference

📍 Must Remember Locations

- GAC (Global Assembly Cache)
    C:\Windows\Assembly
-Stack
   Stores Value Types
   Works on LIFO (Last In First Out)
  Automatic cleanup (method scope based)
-Heap
  Stores Reference Types
  Managed by Garbage Collector

🛠️ Must Remember Tools

* gacutil.exe
 Install / uninstall assemblies in GAC
* sn.exe
 Generate Strong Name key pair
* ngen.exe
  Pre-JIT compilation
  Generates native images
* ildasm.exe
  IL Disassembler
  View IL code & metadata

🔤 Must Remember Full Forms

CLR → Common Language Runtime

IL → Intermediate Language

JIT → Just-In-Time Compiler

CTS → Common Type System

CLS → Common Language Specification

CAS → Code Access Security

GAC → Global Assembly Cache

GC → Garbage Collector


# Tools:

1. GAC install? → gacutil.exe
2. Strong name? → sn.exe
3. Pre-JIT? → ngen.exe



## Notes - cheat  Sheet 
https://docs.google.com/document/d/1cWu17ge1fiX8u-tFNV618LYBpsDBrPmMcCOsFXHCQrQ/edit?usp=sharing



## .NET Framework & Related Concepts - MCQ Based Notes
1. .NET Framework vs .NET Core vs Mono vs Xamarin
Key Differences (MCQ mein frequently aata hai):

1. .NET Framework: Windows-only, full-featured, older version. Example: ASP.NET, WinForms
2. .NET Core: Cross-platform (Windows, Linux, Mac), lightweight, modern. Ab .NET 5+ ban gaya
3. Mono: Open-source implementation of .NET Framework, cross-platform support ke liye
4. Xamarin: Mobile app development (Android, iOS) ke liye, Mono par based hai
5. "ILDASM kya karta hai?" → Shows IL code from assembly
6.  LINQ = Version 3.5
