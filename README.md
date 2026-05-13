# 2a_Stop_and_Wait_Protocol

NAME : JAIRAM J
REG NO : 212225040141
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
```
import socket
import threading
import time

host = "localhost"
port = 8000

frames = ["Hii", "Network", "StopWait", "Protocol"]

def receiver():
    r = socket.socket()
    r.bind((host, port))
    r.listen(1)

    print("📡 Receiver Ready...\n")

    conn, addr = r.accept()

    print("🔗 Connected with", addr)

    while True:
        data = conn.recv(1024).decode()

        if data == "END":
            print("\n🛑 Communication all finished")
            break

        print(f"📥 Frame Received : {data}")

        time.sleep(1)

        conn.send("ACK".encode())

        print("📤 ACK Sent\n")

    conn.close()
    r.close()

def sender():
    time.sleep(2)

    s = socket.socket()
    s.connect((host, port))

    for frame in frames:

        print(f"📤 Sending Frame : {frame}")

        s.send(frame.encode())

        ack = s.recv(1024).decode()

        print(f"✅ {ack} Received\n")

        time.sleep(1)

    s.send("END".encode())

    s.close()

threading.Thread(target=receiver).start()

threading.Thread(target=sender).start()




```
## OUTPUT
<img width="1248" height="573" alt="Screenshot 2026-05-13 151009" src="https://github.com/user-attachments/assets/48f04b07-e544-43df-860d-22e98aa9581a" />

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed.
