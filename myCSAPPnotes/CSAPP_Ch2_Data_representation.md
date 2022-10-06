# Representing and Manipulating Information

[Part I: Program Structure and Execution] : [Ch2: Data Representation]

- 2.1 Infromation Storage
- 2.2 Integer Representations
- 2.3 Integer Arithmetic
- 2.4 Floating Point
- 2.5 Summary

*Two's-complement* encodings are the most common way to represent *signed* integers, that is, numbers that may be either positive or negative.

Floating-point arithmetic is not associative (结合律) due to the finite precision (精度) of the representation. 

Word list
- subtleties 微妙
- auspice 支持 赞助
- culminate in 达到顶点; 以...告终
- verbose 冗长
- tedious 乏味的 单调的
- quotient 商
- remainder 剩余物

## 2.1  Information Storage

### 2.1.1   Hexadecimal Notation

**Practice Problem 2.1** <br>

A. 0x25B9D2 to binary <br>

    0010 0101 1011 1001 1101 0010

B. binary 1010 1110 0100 1001 to hexadecimal <br>

    0xCE49

C. 0xA8B3D to binary

    1010 1000 1011 0011 1101

------------

**Practice Problem 2.2** <br>

Fill in the blank entries in the following table, giving the decimal and dexadecimal representations of different powers of 2:

| n | 2^n (decimal) | 2^n (hexadecimal) |
| - | ----          | ----              |
| 5 | 32            | 0x20              |
| 23 | ? 8,388,608 | ? 0x800000 |
| ? 15 | 32,768 | ? 0x8000 |
| ? 13 | ? 4096 | 0x2000 |
| 12 | ? 2048 | ? 0x1000 |
| ? 6 | 64 | ? 0x40 |
| ? 8 | ? 256 | 0x100 |

------------

**Practice Problem 2.3**

A single byte can be represented by 2 hexadecimal digits. Fill in the missing entries in the following table, giving the decimal, binary, and hexadecimal values of different byte patterns:

| Decimal | Binary | Hexadecimal |
| ----    | ----   | ----        |
| 0 | 0000 0000 | 0x00 |
| 158 | ? 1001 1110 | ? 0x9E |
| 76 | ? 0100 1100 | ? 0x4C |
| 145 | ? 1001 0001 | ? 0x91 |
| ? 174 | 1010 1110 | ? 0xAE |
| ? 60 | 0011 1100 | 0x3C |
| ? 241 | 1111 0001 | 0xF1 |
| ? 117 | ? 0111 0101 | 0x75 |
| ? 189 | ? 1011 1101 | 0xBD |
| ? 245 | ? 1111 0101 | 0xF5 |

----------------

**Practice Problem 2.4**

Without converting the numbers to decimal or binary, try to solve the following arithmetic problems, giving the answers in hexadecimal. *hint:* Jst modify the methods you use for performing decimal addition adn substraction to use base 16.

A. 0x605c + 0x5 = ? 0x6061 <br>

B. 0x605c - 0x20 = ? 0x603c 

C. 0x605c + 32 = ? 0x607c

D. 0x60fa - 0x605c = ? 0x9E

------------

### 2.1.2   Data Sizes

Every computer has a *word size*. indicating the nominal (名义上的) size of pointer data. A 32-bit word size limits the virtual address space to 4 gigabytes (written 4GB), that is , just over 4 x 10^9 bytes. Scaling up to a 64-bit word size leads to a virtual address space of 16 *exabytes* , or 1.84 x 10^19 bytes.

Exabyte (艾字节, EB, 1024^6 bytes or 2^60 bytes, the entire Internet less than 525 EB in 2011).

### 2.1.3   Addressing and Byte Ordering

word list
- convention 惯例
- endian 字节序

Addressing
0x100 0x101 0x102 0x103

Byte Ordering
大端 小端

0x01234567
Big endian: 01 23 45 67
Little endian: 67 45 23 01

Most Intel-compatible machines operate exclusively in little-endian mode. On the other hand, most machines from IBM and Oracle (arising from their acquisition of Sun Microsystems in 2010) operate in big-endian mode. Note that we said "most." The conventions do not split precisely along corporate boundaries. For example, both IBM and Oracle manufacture machines that use Intel-compatible processors and hence are little endian. Many recent microprocessor chips are *bi-endian*, meaning that they can be configured to operate as either little- or big-endian machine. In practice, however, byte ordering becomes fixed once a particular operating system is chosen. For example, ARM microprocessors, used in many cell phones, have hardware that can operate in either little- or big-endian mode, but the two most commmon operating systems for these chips -- Android (from Google) and IOS (from Apple) -- operate only in little-endian mode.

**Aside** Origin of "endian"

disassembler 反编译程序

Byte ordering becomes visible:
1. using network pass code between big-endian and little-endian machines.

2. looking at the byte sequences representing integer data.

3. when programs are written that circumvent the normal type system.

In C lang, this can be done using a *cast* or a *union* to allow an object to be referenced according to a different datat type from which it was created. Such coding tricks are strongly discouraged fro most application programming, but they can be quite useful and even necessary for system-level programming.

This shows C code that uses casting to access and print the byte representations to different program objects. We use typedef to define data type byte_pointer as a pointer to an object of type unsigned char. Such a byte pointer references a sequence of bytes where each byte is considered to be a nonnegative integer. The first routine show_bytes is given the address of a sequence of bytes, indicated by a byte pointer, and a byte count.The byte count is specified as having data type size_t, the preferred data type for expressing the sizes of data structures. It prints the individual bytes in hexadecimal. The C formatting directive %.2x indicates that an integer should be printed in hexadecimal with at least 2 digits.

#include <stdio.h>

typedef unsigned char * byte_pointer;

void show_bytes(byte_pointer start, size_t len) {
    int i;
    for (i = 0; i < len; i++)
        printf(" %.2x", start[i]);
    printf("\n");
}

void show_int(int x) {
    show_bytes((byte_pointer) &x, sizeof(int));
}

void show_float(float x) {
    show_bytes((byte_pointer) &x, sizeof(float));
}

void show_pointer(void *x) {
    show_bytes((byte_pointer) &x, sizeof (void *));
}

useful command: man ascii

**Practice Problem 2.5**

A. LE:78; BE:12

B. LE:78 56; BE: 12 34

C. LE 78 56 34; BE: 12 34 56

**Practice Problem 2.6**

A. 
0000 0000 0010 0111 1100 1000 1111 1000
0100 1010 0001 1111 0010 0011 1110 0000

B.
00000000001 001111100100011111000
  010010100 001111100100011111000 00
21 bits matches. 11 bits not matches.

C. head and tail

### 2.1.4   Representing Strings

**Practice Problem 2.7**

const char *m = "mnopqr";
show_bytes((byte_pointer) m, strlen(m));

6d 6e 6f 70 71 72

### 2.1.5   Representing Code

int sum(int x, int y) {
    return x + y;
}

### 2.1.6   Introduction to Boolean Algebra

This started with the work of George Boole (1815-1864, 49) around 1850(35) and thus is known as *Boolean algebra*. Boole observed that by encoding logic values TRUE and FALSE as binary value 1 and 0, he could formulate an algebra that captures the basic principles of logical resoning.

The simplest Boolean algebra is defined over the two-element set {0, 1}. Figure 2.7 defines several operations in this algebra. Our symbols for representing these operations are chosen to mactch those used by the C bit-level operations, as will be discussed later.

| ~  |    |
| -- | -- |
| 0  | 1  |
| 1  | 0  |

| &    | 0  | 1  |
| ---- | -- | -- |
| 0    | 0  | 0  |
| 1    | 0  | 1  |

| \|   | 0  | 1  |
| ---- | -- | -- |
| 0    | 0  | 1  |
| 1    | 1  | 1  |

| ^    | 0  | 1  |
| ---- | -- | -- |
| 0    | 0  | 1  |
| 1    | 1  | 0  |

Figure 2.7 Operations of Boolean algebra.

Binary values 1 and 0 encode logic values True and False, while operation ~, &, | and ^ encode logical operation NOT, AND, OR, and EXLUSIVE-OR, respectively.

NOT: ¬ ~
AND: ∧ &
OR:  ∨ |
EXCLUSIVE-OR: ⊕ ^

Claude Shannon (1916-2001, 85), who later founded the field of information theory, first made the connection between Boolean algebra and digital logic. In his 1937(21) master's thesis, he showed that Boolean algebra could be applied to the design and analysis of networks of electromechanical relays(继电器). Although computer technology has advanced considerably since, Boolean algebra still plays a central role in the design and analysis of digital systems.

We can extend the four Boolean operations to also operate on *bit vectors*, strings of zeros and ones of some fixed length *w*. We define the operations over bit vectors according to their applications to the matching elements of the arguments. let *a* and *b* denote the bit vectors [a(w-1),a(w-2),...,a(0)] and [b(w-1),b(w-2),...,b0], respectively. We define a & b to also be a bit vector of length *w*, where the *i*th element equals *a*(i) & *b*(i), for (0<=i<*w*). The operations |, ^, and ~ are extended to bit vectors in a similar fashion.

**Web Aside DATA:BOOL**

Boolean operation & distributes over |, written a & (b | c) = (a & b) | (a & c).

In addition, however, Boolean operation | distributes over &, written a | (b & c)= (a | b) & (a | c).

*Boolean ring* have many properties in common with integer arithmetic. a ^ a = 0

(a ^ b) ^ a = b

**Practice Problem 2.8**

a = 0100 1110
b = 1110 0001

~a = 1011 0001
~b = 0001 1110

a & b = 0100 0000
a | b = 1110 1111
a ^ b = 1010 1111

--------------

**Practice Problem 2.9**

| R | G | B | Color | 颜色 |
| 0 | 0 | 0 | Black | 黑色 |
| 0 | 0 | 1 | Blue | 蓝色 |
| 0 | 1 | 0 | Green | 绿色 |
| 0 | 1 | 1 | Cyan | 蓝绿色 |
| 1 | 0 | 0 | Red | 红色 |
| 1 | 0 | 1 | Magenta | 品红；洋红 |
| 1 | 1 | 0 | Yellow | 黄色 |
| 1 | 1 | 1 | White | 白色 |

A.
Black - White
Red - Cyan
Blue - Yellow
Green - Magenta

B.
Blue | Green = 0 1 1 Cyan
Yellow & Cyan = 0 1 0 Green
Red ^ Magenta = 0 0 1 Blue

----------

### 2.1.7   Bit-Level Operations in C

WL
- bitwise 按位
- integral 整数的

**Practice Problem 2.10**
As an app of the property that a^a = 0 for any bit vector a, consider the following program:

void inplace_swap(int *x, int *y) {
    *y = *x ^ *y; 
    *x = *x ^ *y;
    *y = *x ^ *y;
}

As the name implies, we claim that the effect of this procedure is to swap the values stored at the locations denoted by pointer variables x and y. Note that unlike the usual technique for swapping two values, we do not need a third location to temporarily store one value while we are moving the other. There is no performance advantage to this way of swapping; it merely an intellectual amusement.

Starting with values a and b in the locations pointed to by x and y, repectively, fill in the table that follows, giving the values stored at the two locations after each step of the procedure. Use the properties of ^ to show that the desired effect is achieved. Recall that every element is its own additive inverse.

| Step | *x | *y |
| ---- | -- | -- |
| Initially | a | b |
| Step 1 | a | a^b |
| Step 2 | a^a^b | a^b |
| Step 3 | b | a |

-----------

**Practice Problem 2.11**

reverse the elements of an array by swapping elements from opposite ends of the array, working toward the middle.

void reverse_array(int a[], int cnt) {
    int first, last;
    first = 0;
    last = cnt - 1;
    for (; first <= last; first++, last--)
        inplace_swap(&a[first], &a[last]);
}

A. cnt = 2k + 1, what are the values of viriables first and last in the final iteration of function reverse_array?

2 2 

B. Why does this call to function inplace_swap set the array element to 0?

because a^a=0

C. What simple modification to the code for reverse_array would eliminate this problem?

easy. "first < last"

----------------

One common use of bit-level operations is to implement *masking* operations, where a mask is a bit pattern that indicates a selected set of bits within a word. As for an example, the mask 0xFF (having ones for the least significant 8 bits) indicates the low-order byte of a word. The bit level operation x & 0xFF yields a value consisting of the least significant byte of x, but with all other bytes set to 0.

**Practice Problem 2.12**

Write C expressions, in terms of variable x, for the following values. Your code should work for any word size w >= 8. For reference, we show the result of evaluating the expressions for x = 0x87654321, with w = 32.

A. The least significant byte of x, with all other bits set to 0. [0x00000021]

x & 0xFF

B. All but the least significant byte of x complemented, with the least significant byte left unchanged. [0x789ABC21]

(~x) ^ 0xFF

C. The lest significant byte set to all ones, and all other bytes of x left unchanged. [0x876543FF]

x | 0xFF

--------------------

**Practice Problem 2.13**

bis m=1 z=1 

bic m=1 z=0

/* Declarations of functions implementing operations bis and bic */<br>
int bis(int x, int m);<br>
*x | m*
int bic(int x, int m);<br>
*x & ~m*

/* Compute x|y using only calls to functions bis and bic */<br>
int bool_or(int x, int y) {
    int result = *bis(x, y)*;
    return result;
}

int bool_not(int x) {
    int result = *bic(~0, x)*;
    return result;
}

int bool_and(int x, int y) {
    int result = *bic(x, bic(~0, y))*;
    return result;
}

/* Compute x^y using only calls to functions bis and bic */<br>
int bool_xor(int x, int y) {
    int result = *bic(bis(x, y), bic(x, bic(~0, y)))*;
    return result;
}

---------------

### 2.1.8   Logical Operation in C

C also provides a set of *logical* operators ||, &&, and ~, which correspond to the OR, AND and NOT operations of logic.

**Practice Problem 2.14**

a = 0x55 = 0101 0101
b = 0x46 = 0100 0110

a & b = 0100 0100 = 0x44
a | b = 0101 0111 = 0x57
~a | ~b = 1010 1010 | 1011 1001 = 1011 1011 = 0xBB
a & !b = a & 0 = 0
a && b = 0x01
a || b = 0x01
!a || !b = 0
a && ~b = 0x01

-------------

**Practice Problem 2.15**

x == y

bool bool_equivalent(int x, int y)
{
    return *! ~(x ^ (~y))*;
}

--------------

### 2.1.9   Shift Operations in C

C also provides a set of shift operatins for shifting bit patterns to the left and to the right. For an operand x having bit representation [x(w-1), ..., x(0)], the C expresssion x << k yields a value with bit representation [x(w-k-1), ..., x0, 0, ..., 0]. x is shifted k bits to the left, dropping off the k most significant bits and filling the right end with k zeros. The shift amount should be a value between 0 and w-1. Shift operations associate from left to right, so x << j << k is quivalent to (x << j) << k.

There is corresponding right shift operation,written in C as x >> k, but it has a slightly subtle behavior. Generally, machines support two forms of right shift:

*Logical* A logical right shift fills the left end with k zeros, giving a result [0, ..., 0, x(w-1), ... x(k)].

*Arithmetic*. An arithmetic right shift fills the left end with k repetions of the most significant bit, giving a result [x(w-1), ..., x(w-1), ..., x(k)].

| Operation | Value 1 | Value 2 |
| -- | -- | -- |
| x | 0110 0011 | 1001 0101 |
| x << 4 | 0011 0000 | 0101 0000 |
| x >> 4 (l) | 0000 0110 | 0000 1001 |
| x >> 4 (a) | 0000 0110 | 1111 1001 |

Almost all compiler/machine combinations use arithmetic right shifts for signed data, and many programmers assume this to be the case. For unsigned data, on the other hand, right shifts must be logical.

In constrast to C, Java has a precise definition of how right shifts should be performed. The expression x >> k shifts x arithmetically by k positons, while x >>> k shifts it logically.

**Practice Problem 2.16**
Fill in the table below showing the effects of the different shift operations on single-byte quantities. The best way to think aboutshift operations is to work with binary representations. Convert the initial values to binary, perform the shifts, and then convert back tohexadecimal. Each of the answers should be 8 binary digits or 2 hexadecimal digits.

| a | a | a<<2 | a<<2 | Logical a>>3 | Logical a>>3 | Arithmetic a>>3 | Arithmetic a>>3 |
| -- | -- | -- | -- | -- | -- | -- | -- |
| hex | bin | bin | hex | bin | hex | bin | hex |
| 0xD4 | 1101 0100 | 0101 0000 | 0x50 | 0001 1010 | 0x19 | 1111 1010 | 0xF9 |
| 0x64 | 0110 0100 | 1001 0000 | 0x90 | 0000 1100 | 0x0C | 0000 1100 | 0x0D |
| 0x72 | 0111 0010 | 1100 1000 | 0xC8 | 0000 1110 | 0x0E | 0000 1110 | 0x0E |
| 0x44 | 0100 0100 | 0001 0000 | 0x10 | 0000 1000 | 0x08 | 0000 1000 | 0x08 |

----------------

**Aside** 
Shifting by *k*, for large values of *k*

**Aside**
Operator precedence issues with shift operations



## 2.2 Integer Representations

Figure 2.8 Terminology for integer data and arithmetic operations. The subscript *w* denotes the number of bits in the data representation. The "Page" column indicates the page on which the term is defined.

| Symbol | Type | Meaning | Page |
| -- | -- | -- | -- |
| B2Tw | Function | Binary to two's complement | 100 |
| B2Uw | Function | Binary to unsigned | 98 |
| U2Bw | Function | Unsigned to binary | 100 |
| U2Tw | Function | Unisigned to two's complement | 107 |
| T2Bw | Function | Two's complement to binary | 101 |
| T2Uw | Function | Two's complement to Unsigned | 107 |
| TMinw | Constant | Minimum two's-complement value | 101 |
| TMaxw | Constant | Maximum two's-complement value | 101 |
| UMaxw | Constant | Maximum unsigned value | 99 |

### 2.2.1   Integral Data Types 

C support a variety of *integral* data types -- ones that represent finite ranges of integers. These are shown in Figure 2.9 and 2.10, along with the ranges of values they can have for "typical" 32- and 64-bit programs. Each type can specify a size with keyword *char*, *short*, *long*, as well as an indication of whether the represented numbers are all nonnegative (declared as *unsigned*), or possibly negative (the default.) 

### 2.2.2   Unsigned Encoding

#### PRINCIPLE: 
Uniqueness of unsigned encoding
Function B2Uw is a bijection

### 2.2.3   Two's-complement Encodings

#### PRINCIPLE: 
Uniqueness of unsigned encoding
Function B2Tw is a bijection.

**Practice Problem 2.17**

| Hexadecimal | Binary | B2U4 | B2T4 |
| -- | -- | -- | -- |
| 0xA | 1010 | 8+2=10 | -8+2=-6 |
| 0x1 | 0001 | 1 | 1 |
| 0xB | 1011 | 8+2+1=11 | -8+2+1=-5 |
| 0x2 | 0010 | 2 | 2 |
| 0x7 | 0111 | 4+2+1=7 | 4+2+1=7 |
| 0xC | 1100 | 8+4=12 | -8+4=-4 |

-----------

**Practice Problem 2.18**

In ch3, we'll look at listings (表) generated by a *disassembler*, a program that converts an executable program file back to a more readable ASCII form. These files contain many hexadecimal numbers, typically representing values in two's-complement form. Being able to recognize these numbers and understand their significance (for example, whether they are negative or positive) is an important skill.

For the lines labedled A-I (on the right) in the following listing, convert the hexadecimal values (in 32-bit two's-complement form) shown to the right of the instruction names (sub, mov, and add) into their decimal equivalents:

A. 0x2e0 = 0...10 1110 0000 = 2^9 + 2^7 + 2^6 + 2^5 = 512 + 128 + 64 + 32 = 736

B. -0x58 = (T's-C) 0xA8 = 1010 1000 = -2^7 + 2^5 + 2^3 = -128 + 32 + 8 = -88

C. 0x28 = 0010 1000 = 2^5 + 2^3 = 32+8=40

D. -0x30 = (T) 0xD0 = 1011 0000 = -2^7 + 2^5 + 2^4 = -128 + 32 + 16 = -80

E. 0x78 = 0111 1000 = 7*16 + 8 = 120

F. 0x88 = 0...0 1000 1000 = 8*16+8=128+8=136

G. 0x1f8 = 0...01 1111 1000 = (1 * 16 + 15) * 16 + 8 = 31 * 16 + 8 = 496 + 8 = 504

H. 0xC0 = 0...0 1100 0000 = 12*16 = 192

I. -0x48 = -(4*16+8) = (C) 0xb8 = 1011 1000 = -2^7 + 2^5 + 2^4 + 2^3 = -128 + 32 + 16 + 8 = -72

-----------

### 2.2.4   Conversions between Signed and Unsigned

**Practice Problem 2.19**

| Hexadecimal | Binary | B2U4 | B2T4 |
| -- | -- | -- | -- |
| 0xA | 1010 | 8+2=10 | -8+2=-6 |
| 0x1 | 0001 | 1 | 1 |
| 0xB | 1011 | 8+2+1=11 | -8+2+1=-5 |
| 0x2 | 0010 | 2 | 2 |
| 0x7 | 0111 | 4+2+1=7 | 4+2+1=7 |
| 0xC | 1100 | 8+4=12 | -8+4=-4 |

| x | (T's-c)Binary | T2U4(x) |
| -- | -- | -- |
| -1 | 1111 | 15 |
| -5 | 1011 | 11 |
| -6 | 1010 | 10 |
| -4 | 1100 | 12 |
|  1 | 0001 | 1  |
| 8 | can't | 8 |

----------

**Practice Problem 2.20**

----------

### 2.2.5   Signed versus Unsigned in C

**Practice Problem 2.21**

| Expression | Type | Evaluation |
| -- | -- | -- |
| -2147483647-1 == 2147483648U | Unsigned | TRUE |
| -2147483647-1 < 2147483647 | Signed | TRUE |
| -2147483647-1U < 2147483647 | Unsigned | False |
| -2147483647-1 < -2147483647 | Signed | True |
| -2147483647-1U < -2147483647 | Unsigned | False |

----------

**Web Aside DATA:TMIN** Writing TMin in C

### 2.2.6   Expanding the Bit Representation of a Number

**Practice Problem 2.22**

-----------

**Practice Problem 2.23**

int fun1(unsigned word) {
    return (int) ((word << 24) >> 24);
}

int fun2(unsigned word) {
    return ((int) word << 24) >> 24);
}

A. 

| w in hex | fun1(w) | fun2(w) |
| ---- | ------- | ------- |
| 0x00000076 | 0x00000076 | 0x00000076 |
| 0x87654321 | 0x00000021 | 0x00000021 |
| 0x000000C9 | 0x000000C9 | 0xFFFFFFC9 |
| 0xEDCBA987 | 0x00000087 | 0xFFFFFF87 |

B.

I don't see them useful.

----------

### 2.2.7   Truncating Numbers

**Practice Problem 2.24**

4-bit to 3-bit.

| hex | hex | unsigned | unsigned | 2scomplet | 2scomplet |
| -- | -- | -- | -- | -- | -- |
| original | truncated | original | truncated | original | truncated |
| 1 | 1 | 1 | 1 | 1 | 1 |
| 3 | 3 | 3 | 3 | 3 | 3 |
| 5 | 5 | 5 | 5 | 5 | -3 |
| C | 4 | 12 | 4 | 12 | -4 |
| E | 6 | 14 | 6 | 16 | -2 |

Explain how Equation 2.9 and 2.10 apply to these cases.

--------------

### 2.2.8   Advice on Signed versus Unsigned

**Practice Problem 2.25**

/* WARNING: This is buggy code */

float sum_elements(float a[], unsigned length) {
    int i;
    float result = 0;

    for (i = 0; i <= length-1; i++)
        result += a[i];
    return result;
}

when run with argument length equal to 0, "i <= length-1" --> "0 <= 0-1" which is ilegal.

**Practice Problem 2.26**

/* Prototype for library function strlen */

size_t strlen(const char *s);

/* Determine whether string s is longer than string t */

/* WARNING: This function is buggy */

int strlonger(char *s, char *t) {
    return strlen(s) - strlen(t) > 0;
}

A. For what cases will this func produce an incorrect result?

when t is longer than s.

B. Explain how this incorrect result comes about.

it's because they are unsigned. it can't below 0;

C. Show how to fix the code so that it will work reliably.

"strlen(s) - strlen(t) > 0" --> "strlen(s) > strlen(t)"

-------------

## 2.3  Integer Arithmetic

### 2.3.1   Unsigned Addition

**Aside** Security vulnerability in getpeername

**Practice Problem 2.27**

/* Determine whether arguments can be added without overflow */

int uadd_ok(unsigned x, unsigned y)
{
    unsigned s = x + y;
    if (s < x)
        return 0;
    else
        return 1;
}

----------

Modular addition forms a mathematical structure known as an *abellian group*, named after the Norwegian mathematician Niels Henrik Abel (1802-1829). That is, it is commutative (that's where the "abelian" part comes in) and associative; it has an identity element 0, and every element has an additive inverse. 

**Practice Problem 2.28**

| x | x | -x | -x |
| -- | -- | -- | -- |
| hex | dec | dec | hex |
| 1 | 1 | 15 | F |
| 4 | 4 | 12 | C |
| 7 | 7 | 9 | 9 |
| A | 10 | 6 | 6 |
| E | 14 | 2 | 2 |

--------------

### 2.3.2   Two's-Complement Addition

**Practice Problem 2.29**

x       y       x+y     x+(t5)y case
-12     -15     -37     5       1
10100   10001   00101   00101   1
-8      -8      -16     -16     2
11000   11000   10000   10000   2
-9      8       -1      -1      2
10111   01000   11111   11111   2
2       5       7       7       3
00010   00101   00111   00111   3
12      4       16      -16     4
01100   00100   10000   10000   4

------------

**Practice Problem 2.30**

int tadd_ok(int x, int y) 
{
    int s;
    s = x + y;
    if (x > 0 && y > 0 && s < 0)
        return 0;
    else if (x < 0 && y < 0 && s > 0)
        return 0;
    else
        return 1;
}

-----------------

**Practice Problem 2.31**

still overflows and generate false result.

----------------

**Practice Problem 2.32**

You are assigned the task of writing code for a function tsub_ok, with arguments x and y, that will return 1 if computing x-y does not cause overflow. Having just written the code for Problem 2.30, you write the following:

/* Determine whether arguments can be subtracted without overflow */<br>
/* WARNING: This code is buggy. */<br>
int tsub_ok(int x, int y) {
    return tadd_ok(x, -y);
}

For what values of x and y will this function give incorrect results? Writing a correct version of this function is left as an exercise (Problem 2.74)

0001 (1) + 1000 (-8) = 1001 (-7)

1001 (-7) - 1000(-8) = 0001 (1)

answer: when y = Tmin,  will cause overflow.

------------------

### 2.3.3   Two's-Complement Negation

We can see that every number x in the range Tmin <= x <= Tmax has an additive inverse under +(t,w), which we denote -(t,w) as follows:

for all x satisfy: Tmin <= x <= Tmax, we have:

-x = TMin , when x = Tmin;
-x = -x , when x > Tmin;

**Practive Problem 2.33**

w = 4; -(t,w);

| x | x | -x | -x |
| - | - | -- | -- |
| hex | dec | dec | hex |
| 2 | 2 | -2 | -2 |
| 3 | 3 | -3 | -3 |
| 9 | -7 | 7 | 7 |
| B | -5 | 5 | 5 |
| C | -4 | 4 | 4 |

-----------------

**Web Aside DATA:TNEG** Bit-level representation of two's-complement negation

------------------

### 2.3.4   Unsigned Multiplication

### 2.3.5   Two's-Complement Multiplication

**Practice Problem 2.34**

mode    x   y   x`*`y     truncated x`*`y
unsigned 4 100 5 101 20 10100 4 100
t's-comp -4 100 -3 101 12 01100 -4 100
unsigned 2 010 7 111 14 01110 6 110
t's-comp 2 010 -1 111 -2 11110 -2 110
unsigned 6 110 6 110 36 100100 4 100
t's-comp -2 110 -2 110 4 000100 -4 100

------------------

**Practice Problem 2.35**

/* Determine whether arguments can be multiplied without overflow */ <br>
int tmult_ok(int x, int y) {
    int p = x * y;
    // Either x is zero , or dividing p by x gives y
    return !x || p/x == y;
}

--------------

**Practice Problem 2.36**

int tmult_ok(int x, int y) {
    int64_t p;
    int64_t xx = x;
    int64_t yy = y;
    p = xx * yy;
    return x > 0xFFFFFFFF000000 && x < 0x000000007FFFFFFF;
}

---------------

**Practice Problem 2.37**

patching 修补

**Aside** Security vulnerability in the XDR library

uint64_t asize = 
    ele_cnt * (uint64_t) ele_size;
void *result = malloc(asize);

Recall that the argument to malloc has type size_t;

A. No, it doesn't.

B. Just use size_t; And report an error when overflows.

----------------

### 2.3.6   Multiplying by Constants

**Practice Problem 2.38**

a * (2^n)

a * (2^n + 1)

---------------

**Practice Problem 2.39**

How could we modify the expression for form B for the case where bit position n is the most significant bit?

? (x << n) - (x << m);
? ~x + (x << m)

-------------

**Practice Problem 2.40**

K 

x * K 

| K | Shifts | Add/Subs | Expression |
| - | ------ | -------- | ---------- |
| 7 | 1 | 1 | (x << 3) - x |
| 30 | 4 | 3 | (x<<4)+(x<<3)+(x<<2)+(x<<1) |
| 28 | 2 | 1 | (x << 5) - (x << 2) |
| 55 | 2 | 2 | (x<<6) - (x<<3) - x |

-----------------

**Practice Problem 2.41**

For a run of ones starting at bit bit position n down to bit position m (n>=m), we saw that we can generate two forms of code, A and B. How should the compiler decide which form to use?

Answer: To see which one is fast.

----------------

### 2.3.7   Dividing by Powers of 2

**Practice Problem 2.42**

int div16(int x) {
    return (x > 0? x : x+(1 << k)-1 ) >> k;
}

------------

**Practice Problem 2.43**

M = 2^5 - 1 = 32 - 1 = 31

N = 2^3 = 7 + 1 = 8

-------------

### 2.3.8   Final Thoughts on Integer Arithmetic

As we have seen, the integer arithmetic performed by computers is really a form of modular arithmetic. The finite word size used to represent numbers limits the range of possible values, and the resulting operations can overflow. We have also seen that the two's-complement representation provides a clever way to represent both negative and positive values, while using the same bit-level implementations as are used to perform unsigned arithmetic -- operations such as addition, subtraction, multiplication, and even division have either identical or very similar bit-level behaviors, whether the operands are in unsigned or two's-complement form.

We have seen that some of the conventions in the C language can yield some surprising results, and these can be sources of bugs that are hard to recognize or understand. We have especially seen that the unsigned data type, while conceptually straightforward, can lead to behaviors that even experienced programmers do not expect. We have also seen that this data type can arise in unexpected ways -- for example, when writing integer constants and when invoking library routines.

**Practice Problem 2.44**

A. True 1

B. True 1

C. x = 2^15 + 4;  0x0...01...1
    x * x = 2 ^ 30 + 16 + 2 * 4 * 2^15
    overflow.

D. x < 0 || -x <= 0
    TRUE

E. x > 0 || -x >= 0
    False 
    when x = 0x80...0, -x = 0x80..0 < 0;

F. x+y == uy+ux
    TRUE

G. x*~y + uy*ux == -x
    ? (~y + uy) = -1
    x * (1...1) = -x
    TRUE
    
------------------

## 2.4  Floating Point

