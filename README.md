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

CLIENT:
```
import socket
s=socket.socket()
s.bind(('localhost',8000))
s.listen(5)
c,addr=s.accept()
while True:
    i=input("Enter a data: ")
    c.send(i.encode())
    ack=c.recv(1024).decode()
    if ack:
        print(ack)
        continue
    else:
        c.close()
        break
```
SERVER:
```
import socket
s=socket.socket()
s.connect(('localhost',8000))
while True:
    print(s.recv(1024).decode())
    s.send("Acknowledgement Recived".encode())
``` 
        

## OUTPUT

CLIENT:
![CLIENT EXP2 A](https://github.com/user-attachments/assets/83ce38f0-b46b-4349-a9f4-659e2f60d0b9)

SERVER:
![SERVER EXP2 A](https://github.com/user-attachments/assets/d7866ea4-e7fe-4055-9bf2-67c60e18e9fd)




## RESULT
Thus, python program to perform stop and wait protocol was successfully executed.
