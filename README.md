# 5a_Create_Socket_for_HTTP_for_webpage_upload_and_download
## AIM :
To write a PYTHON program for socket for HTTP for web page upload and download
## Algorithm

## ALGORITHM

1. Start the program.

2. Create socket in server and client.

3. Bind server with host and port number.

4. Server waits for client connection.

5. Client connects to the server.

6. Client selects:
   - Download (GET)
   - Upload (POST)

7. If GET request:
   - Server reads index.html
   - Sends HTML content to client

8. If POST request:
   - Client sends data
   - Server stores data in upload.txt

9. Display response message.

10. Close client and server connection.

11. Stop the program.
## Program
## Client-side
```
import socket

s = socket.socket()

s.connect(("localhost", 3024))

print("1.Download")
print("2.Upload")

ch = input("Enter choice: ")

if ch == "1":

    req = "GET / HTTP/1.1\nHost: localhost\n\n"

    s.send(req.encode())

    print(s.recv(4096).decode())

else:

    msg = input("Enter data: ")

    req = "POST / HTTP/1.1\nHost: localhost\n\n" + msg

    s.send(req.encode())

    print(s.recv(1024).decode())

s.close()

```
## Server Side

```
import socket

s = socket.socket()
s.bind(("localhost", 3024))
s.listen(1)

print("Server Running...")

while True:

    c, addr = s.accept()

    req = c.recv(1024).decode()

    print("Request received")

    if "GET" in req:

        f = open("indeex.html", "r")
        data = f.read()

        response = "HTTP/1.1 200 OK\n\n" + data

        c.send(response.encode())

        f.close()

        print("HTML page sent")

    else:

        msg = req.split("\n\n")[1]

        f = open("upload.txt", "w")
        f.write(msg)
        f.close()

        c.send("HTTP/1.1 200 OK\n\nData Uploaded".encode())

        print("Data uploaded")

    c.close()

```
## OUTPUT


<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/47b2101d-23b7-4ea2-a7bf-7b8363120b4e" />

<img width="626" height="924" alt="image" src="https://github.com/user-attachments/assets/d754025a-efbb-4047-a8ce-c0b94c9cf8e6" />

<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/f5677ca4-c166-4457-a0cc-9e90154bd947" />



## Result
Thus the socket for HTTP for web page upload and download created and Executed
