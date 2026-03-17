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
## server-side.py
```
import socket

HOST = "127.0.0.1"
PORT = 8000

server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
server.bind((HOST, PORT))
server.listen(1)

print("Server is listening...")

conn, addr = server.accept()
print("Connected with", addr)

while True:
    data = conn.recv(1024)

    if not data:
        print("Client disconnected")
        break

    message = data.decode()
    print("Received:", message)

    if message.lower() == "exit":
        conn.send("BYE".encode())
        print("Closing connection...")
        break

    conn.send("ACK".encode())

conn.close()
server.close()
```
## client-side.py
```
import socket

HOST = "127.0.0.1"
PORT = 8000

client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
client.connect((HOST, PORT))
client.settimeout(3)

print("Connected to server")

while True:
    msg = input("Enter message (or 'exit'): ")
    client.send(msg.encode())

    try:
        response = client.recv(1024).decode()
        print("Server response:", response)

        if response == "BYE":
            print("Server closed the connection")
            break

    except socket.timeout:
        print("Timeout! No response from server")

    if msg.lower() == "exit":
        break

client.close()
```
## OUTPUT
<img width="867" height="123" alt="image" src="https://github.com/user-attachments/assets/eacdb095-670d-4e26-ad80-3fa2290b46fe" />
<img width="811" height="188" alt="image" src="https://github.com/user-attachments/assets/6a845671-8586-48b8-a1a4-913391e60e67" />

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed.
