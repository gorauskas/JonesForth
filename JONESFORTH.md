# Jones' Forth

A FORTH compiler and tutorial - a step-by-step implementation of a [FORTH language](https://web.archive.org/web/20090209211708/http://en.wikipedia.org/wiki/Forth_(programming_language)) system.

To comment on this please use this [LtU forums thread on this FORTH](https://web.archive.org/web/20090209211708/http://lambda-the-ultimate.org/node/2452). There are also some exercises suggested in that thread.

## Download

The tutorial is now in two parts:

1. [jonesforth.s.txt](https://raw.githubusercontent.com/nixdork/JonesForth/main/jonesforth.S) -> rename to jonesforth.S (capital letter S) after downloading
2. [jonesforth.f.txt](https://raw.githubusercontent.com/nixdork/JonesForth/main/jonesforth.f) -> rename to jonesforth.f after downloading

It requires a Linux system, i386 or compatible processor, and gas (the GNU assembler).

The entire system is in the public domain.

## Articles

* [Mac OS X / PowerPC port of the assembler code](https://web.archive.org/web/20090209211708/http://www.lshift.net/blog/2007/10/04/jonesforth-ported-to-powerpc-and-mac-os-x)
* http://weblog.raganwald.com/2007/10/until-you-understand-how-forth-is.html
* http://ndanger.org/blog/2007/10/18/adventures-in-forth/
* http://www.bentwookie.org/blog/kragen-hacks/2007-November/000467.html
* http://c2.com/cgi/wiki?ForthLanguage
* [Forth compilers page](https://web.archive.org/web/20090209211708/http://www.forth.org/compilers.html)
* [Discussion and criticism of the implementation](https://web.archive.org/web/20090209211708/http://lukego.livejournal.com/12774.html)

## Papers

[Optimizing indirect branch prediction accuracy in virtual machine interpreters](https://web.archive.org/web/20090209211708/http://portal.acm.org/citation.cfm?id=1286821.1286828&coll=GUIDE&dl=GUIDE&idx=J783&part=journal&WantType=Journals&title=TOPLAS&CFID=15151515&CFTOKEN=6184618) - Interesting paper on why threaded code interpreters don't perform well on processors with ordinary Branch Prediction Tables (and how to improve the situation)

## Examples

Starting with JONESFORTH >= 37, this FORTH implements much of what you would expect in a basic FORTH, and some advanced words like SEE (the decompiler), VALUE, CASE...ENDCASE, etc. Each word is fully explained, even the most complex ones, with a lengthy introduction and plenty of comments in the code.

The following are example command invocations:

```
255 HEX . CR
FF
```
```
1 2 3 4 5 .S CR ROT .S CR
5 4 3 2 1 
4 3 5 2 1
```
```
: TEST
  CASE
  ( keys )
  [ CHAR q ] LITERAL OF ." key: q" CR ENDOF
  [ CHAR s ] LITERAL OF ." key: s" CR ENDOF
  ( default case: )
  ." default: " DUP EMIT CR
  ENDCASE
;
116 TEST
default: t
115 TEST
key: s
114 TEST
default: r
```
```
: HELLO ." Hello, world!" CR ; SEE HELLO 
: HELLO S" Hello, world!" TELL CR ;
```
```
SEE ?IMMEDIATE
: ?IMMEDIATE 4+ C@ F_IMMED AND ;
```
```
0 64 DUMP
      0 8D 6D FC 89 75  0 83 C0  4 89 C6 AD FF 20 FC 89 .m..u........ ..
     10 25 18 10  0  0 BD  0 40  0  0 BE  0  5  0  0 AD %......@........
     20 FF 20 66 90 58 50 50 AD FF 20 66 90 58 AD FF 20 . f.XPP.. f.X.. 
     30 58 5B 50 53 AD FF 20 90 8B 44 24  4 50 AD FF 20 X[PS.. ..D$.P..
```
```
30 VALUE VAL
SEE VAL
: VAL 30 ;
: TEST TO VAL ;
SEE TEST
: TEST 21152 ! ;
20 TEST
VAL . CR
20 
SEE VAL
: VAL 20 ;
```
```
WORDS
INLINE (INLINE) RDTSC RDTSC POP PUSH EDI ESI EBP ESP EBX EDX ECX EAX ;CODE NEXT
PERROR READ-FILE CLOSE-FILE CREATE-FILE OPEN-FILE R/W R/O
MORECORE BRK UNUSED GET-BRK BYE ENVIRON ARGV ARGC CSTRING
STRLEN Z" PRINT-STACK-TRACE ABORT THROW CATCH EXCEPTION-MARKER
['] :NONAME SEE CFA> ENDCASE ENDOF OF CASE DUMP FORGET WORDS
?IMMEDIATE ?HIDDEN ID. +TO TO VALUE VARIABLE CELLS ALLOT CONSTANT
." S" C, ALIGN ALIGNED DEPTH WITHIN ? U. . .R U.R UWIDTH .S U.
HEX DECIMAL SPACES PICK TUCK NIP ( UNLESS REPEAT WHILE AGAIN
UNTIL BEGIN ELSE THEN IF RECURSE [COMPILE] '.' '-' '0' 'A' '"'
')' '(' ';' ':' LITERAL NOT FALSE TRUE NEGATE 2/ 2* 2DROP 2DUP
SPACE CR BL '\n' MOD / SYSCALL0 SYSCALL1 SYSCALL2 SYSCALL3
EXECUTE CHAR INTERPRET QUIT TELL LITSTRING 0BRANCH BRANCH ' HIDE
HIDDEN IMMEDIATE ; : ] [ , CREATE >DFA >CFA FIND NUMBER WORD EMIT
KEY DSP! DSP@ RDROP RSP! RSP@ R> >R O_NONBLOCK O_APPEND O_TRUNC
O_EXCL O_CREAT O_RDWR O_WRONLY O_RDONLY SYS_BRK SYS_CREAT
SYS_WRITE SYS_READ SYS_CLOSE SYS_OPEN SYS_EXIT F_LENMASK
F_HIDDEN F_IMMED DOCOL R0 VERSION BASE S0 LATEST HERE STATE
CMOVE C@C! C@ C! -! +! @ ! LIT EXIT INVERT XOR OR AND 0>= 0<=
0> 0< 0<> 0= >= <= > < <> = /MOD * - + 4- 4+ 1- 1+ ?DUP -ROT
ROT OVER DUP SWAP DROP
```
