All we gotta do is to get 4 numbers, sum them up and send the solution to get the pass for level1;
The thing we have to know that information is transferred over the net in Big-Endian notation, but i'm running on intel cpu, where Little-Endian is a standard. So, we'll have to convert from one endianess to another.
Let's write some code:

```python
import socket
import struct

s = socket.socket (socket.AF_INET, socket.SOCK_STREAM)
s.connect (("vortex.labs.overthewire.org", 5842))
out = 0

for i in range (0, 4):
    t = s.recv(4)
    up = struct.unpack("<I", t)[0]
    out += up
g = struct.pack("<I", out)
s.send(str(g) + '\n')
t = s.recv(512)
print t
```
