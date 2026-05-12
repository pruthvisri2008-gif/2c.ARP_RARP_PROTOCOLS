# 2c.SIMULATING ARP /RARP PROTOCOLS
## AIM
To write a python program for simulating ARP protocols using TCP.
## ALGORITHM:
## Client:
1. Start the program
2. Using socket connection is established between client and server.
3. Get the IP address to be converted into MAC address.
4. Send this IP address to server.
5. Server returns the MAC address to client.
## Server:
1. Start the program
2. Accept the socket which is created by the client.
3. Server maintains the table in which IP and corresponding MAC addresses are
stored.
4. Read the IP address which is send by the client.
5. Map the IP address with its MAC address and return the MAC address to client.
P
## PROGRAM - ARP
server.py
~~~
import socket

s = socket.socket()

s.bind(('localhost', 8000))

s.listen(5)

print("Server is waiting for connection...")

c, addr = s.accept()

print("Connected to:", addr)

address = {
    "165.165.80.80": "6A:08:AA:C2",
    "165.165.79.1": "8A:BC:E3:FA",
    "169.254.161.184": "FC:6D:77:6C:71:A9"
}

while True:
    ip = c.recv(1024).decode()

    if not ip:
        break

    if ip in address:
        c.send(address[ip].encode())
    else:
        c.send("Not Found".encode())

c.close()
~~~
client.py

~~~
import socket

s = socket.socket()

s.connect(('localhost', 8000))

while True:
    ip = input("Enter Logical Address: ")

    s.send(ip.encode())

    mac = s.recv(1024).decode()

    print("MAC Address:", mac)
~~~
## OUPUT - ARP
<img width="1600" height="338" alt="Cn exp02c1" src="https://github.com/user-attachments/assets/6aa44a44-02eb-4273-82aa-0670ae6efb6a" />

## PROGRAM - RARP
server.py
~~~


import socket

s = socket.socket()

s.bind(('localhost', 5000))

s.listen(5)

print("Server is waiting for connection...")

c, addr = s.accept()

print("Connected to:", addr)

address = {
    "6A:08:AA:C2": "165.165.80.80",
    "8A:BC:E3:FA": "165.165.79.1",
    "FC:6D:77:6C:71:A9": "169.254.161.184"
}

while True:
    mac = c.recv(1024).decode()

    if not mac:
        break

    if mac in address:
        c.send(address[mac].encode())
    else:
        c.send("Not Found".encode())

c.close()
~~~
client.py
~~~

import socket

s = socket.socket()

s.connect(('localhost', 5000))

while True:
    mac = input("Enter MAC Address: ")

    s.send(mac.encode())

    ip = s.recv(1024).decode()

    print("IPv4 Address:", ip)

~~~
## OUPUT -RARP
<img width="1600" height="335" alt="CN exp02c" src="https://github.com/user-attachments/assets/7c303704-652c-4d27-993a-c9b791adf5bc" />


## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
