# Buffer_Overflow
Exploiting an application vulnerable to buffer overflow

Run Python 'fuzzer.py' script to find crash point and update offset value in exploit.py to crash point value.

Run !mona findmsp -distance <msf-pattern_create length> in Immunity to find OFFSET VALUE. Update exploit.py script offset value with this value. Set RETN value in exploit.py "B" * 4 to overwrite EIP value '/x42/x42/x42/x42'


