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
client.py
import socket

c = socket.socket()
c.connect(('localhost', 8000))
c.settimeout(5)

while True:
    msg = input("Message: ")
    c.send(msg.encode())

    if msg == "exit":
        break

    try:
        if c.recv(1024).decode() == "ACK":
            print("ACK received")
    except socket.timeout:
        print("No ACK, retransmitting...")

c.close()

server.py
import socket
s = socket.socket()
s.bind(('localhost',8002))
s.listen(5)
c, addr = s.accept()
ListSize = int(input("Enter the number of frames to send : "))
List = list(range(ListSize))
WindowSize = int(input("Enter Window Size : "))
st, i = 0, 0
while True:
    while(i < ListSize):
        st += WindowSize
        c.send(str(List[i:st]).encode())
        Acknowledgment = c.recv(1024).decode()
        if Acknowledgment:
            print(Acknowledgment)
            i+=st
## OUTPUT
<img width="1902" height="1022" alt="Screenshot 2026-05-21 133857" src="https://github.com/user-attachments/assets/4da41a60-fdb9-4d9d-8976-06d522ce343a" />

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed.
