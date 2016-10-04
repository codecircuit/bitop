# BIts TO character Pack (bitop) Library

C++ lacks of dynamic type casting, which represents a difficulty when
dealing with unknown types at compile time. E.g. do you want to
process data, which can have various types (int, float, double,...) and want
a general interface to process that data? Then bitop is the library of
your choice.

You can save any built in data type:
```cpp
int i;
double d;
float f;

charPack cp_i(i);
charPack cp_d(d);
charPack cp_f(f);

cp_i.asInt() == i;            // evaluates to true
cp_d.asDouble_IEEE754() == d; // evaluates to true
cp_f.asFloat_IEEE754() == f;  // evaluates to true
```
The library assumes the usage of IEEE754 floating point numbers.  
Moreover you can save data of unknown type if you know the size:
```cpp
int i;
double d;
float f;

void* p_i = &i;
void* p_d = &d;
void* p_f = &f;

charPack cp_i(p_i, sizeof(int)*8);    // size in bits
charPack cp_d(p_d, sizeof(double)*8); // size in bits
charPack cp_f(p_f, sizeof(float)*8);  // size in bits

cp_i.asInt() == i;            // evaluates to true
cp_d.asDouble_IEEE754() == d; // evaluates to true
cp_f.asFloat_IEEE754() == f;  // evaluates to true
```
The given class can save bits from a certain memory location and
converts the bits to a vector of characters to save them internally. You
can access every bit of the `vector<unsigned char>`, where the highest
index denotes the highest bytes, e.g. you save 16 bits and covert them
to an integer:

Representation       | Values                              | Values                               |
:--------------------|:-----------------------------------:|:------------------------------------:|
Memory               |`0   1   0   1   0   0   0   1`&nbsp;|&nbsp;` 1   0   0   0   0   1   0   1`|
Vector element       |                 [1]                 |                  [0]                 |
If converted to int  |          2^14 + 2^12 + 2^8 +        |            2^7 + 2^2 + 2^0           |

The code comments obey doxygen rules, thus building your own
documentation is recommended.
