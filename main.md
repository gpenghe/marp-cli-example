---
marp: true
size: 16:9
title: Embedded C Coding Standard
description: for Visualization Team
theme: default
paginate: true
_paginate: false
auto-scaling: true
inlineSVG: true
---

## **Rule 1.1: Which C?**

1.1.a. All programs shall be written to comply with the C99 version of the ISO C Programming Language Standard.3

1.1.b. Whenever a C++ compiler is used, appropriate compiler options shall be set to restrict the language to the selected version of ISO C.

1.1.c. The use of proprietary compiler language keyword extensions, #pragma, and inline assembly shall be kept to the minimum necessary to get the job done and be localized to a small number of device driver modules that interface directly to hardware.

1.1.d. Preprocessor directive #define shall not be used to alter or rename any keyword or other aspect of the programming language.

### Reasoning

To clearly define the rules in the rest of this standard, it is important that we first agree on the baseline programming language specification.

### Example

```C
#define begin { // Don’t do something like this...
#define end } // ... nor this.
...
    for (int row = 0; row < MAX_ROWS; row++) 
    begin
        ...
    end                 // Let C be C, not some language you once loved.
```

### Enforcement

These rules shall be enforced via compiler setup and code reviews.

---

## **Rule 1.2: Line Widths**

The width of all lines in a program shall be limited to a maximum of 80 characters.

### Reasoning

From time-to-time, peer reviews and other code examinations are conducted on printed pages. To be useful, such print-outs must be free of distracting line wraps as well as missing (i.e., past the right margin) characters. Line width rules also ease on-screen side-by-side code differencing.

### Enforcement

Violations of this rule shall be detected by an automated scan during each build.

---

## **Rule 1.3: Braces**

1.3.a. Braces shall always surround the blocks of code (a.k.a., compound statements), following if, else, switch, while, do, and for statements; single statements and empty statements following these keywords shall also always be surrounded by braces.

1.3.b. Each left brace ({) shall appear by itself on the line below the start of the block it opens. The corresponding right brace (}) shall appear by itself in the same position the appropriate number of lines later in the file.

### Reasoning

There is considerable risk associated with the presence of empty statements and single statements that are not surrounded by braces. Code constructs like this are often associated with bugs when nearby code is changed or commented out. This risk is entirely eliminated by the consistent use of braces. The placement of the left brace on the following line allows for easy visual checking for the corresponding right brace.

### Example

```C
{
    if (depth_in_ft > 10) dive_stage = DIVE_DEEP; // This is legal... 
    else if (depth_in_ft > 0)
        dive_stage = DIVE_SHALLOW;                 // ... as is this.
    else
    {                       // But using braces is always safer.
        dive_stage = DIVE_SURFACE;
    }
    ...
}
#define begin { // Don’t do something like this...
#define end } // ... nor this.
...
    for (int row = 0; row < MAX_ROWS; row++) 
    begin
        ...
    end                 // Let C be C, not some language you once loved.
```

### Enforcement

Violations of this rule shall be detected by an automated scan during each build.
The presence of a left brace after each if, else, switch, while, do, and for shall be enforced by an automated tool at build time. The same tool or another (such as a code beautifier) shall be used to enforce the alignment of braces.

---
