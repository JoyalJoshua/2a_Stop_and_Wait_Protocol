```
name: Joyal Joshua
reg no: 212225040162
```
# 2a_Stop_and_Wait_Protocol
## AIM 
To write a python program to perform stop and wait protocol
## ALGORITHM
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM
### server.py:
```
import socket

server = socket.socket()
server.bind(('localhost', 8000))
server.listen(1)
print("Server is listening...")
conn, addr = server.accept()
print(f"Connected with {addr}")

while True:
    data = conn.recv(1024).decode()

    if data:
        print(f"Received: {data}")
        conn.send("ACK".encode())

        if data.lower() == 'exit':  
            print("Connection closed by client")
            conn.close()
            break


```
### client.py:
```

import socket
import time

client = socket.socket()
client.connect(('localhost', 8000))
client.settimeout(5)  

while True:
    msg = input("Enter a message (or type 'exit' to quit): ")

    client.send(msg.encode())  

    if msg.lower() == 'exit':  
        print("Connection closed by client")
        client.close()
        break

    try:
        ack = client.recv(1024).decode()
        if ack == "ACK":
            print(f"Server acknowledged: {ack}")
    except socket.timeout:
        print("No ACK received, retransmitting...")
        continue  

```
## OUTPUT
### server:

<img width="1920" height="1080" alt="Screenshot 2026-01-30 181438" src="https://github.com/user-attachments/assets/df8c76cf-2df2-429a-a5e6-f30ac1835ec3" />

### client:

<img width="1920" height="1080" alt="Screenshot 2026-01-30 181448" src="https://github.com/user-attachments/assets/deb1098c-7ab8-4a1d-afdd-d3218254c1d4" />

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed.
