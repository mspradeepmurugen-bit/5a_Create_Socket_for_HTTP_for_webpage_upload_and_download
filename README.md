# 5a_Create_Socket_for_HTTP_for_webpage_upload_and_download
## AIM :
To write a PYTHON program for socket for HTTP for web page upload and download
## Algorithm

1.Start the program.
<BR>
2.Get the frame size from the user
<BR>
3.To create the frame based on the user request.
<BR>
4.To send frames to server from the client side.
<BR>
5.If your frames reach the server it will send ACK signal to client otherwise it will send NACK signal to client.
<BR>
6.Stop the program
<BR>
## Program
SERVER
```
import socket

s = socket.socket()
s.bind(("localhost",3024))
s.listen(1)

print("Server running...")

while True:
    c,addr = s.accept()
    
    request = c.recv(1024).decode()
    print("Request received")

    if "GET" in request:
        f = open("index.html","r")
        data = f.read()
        f.close()

        response = "HTTP/1.1 200 OK\n\n" + data
        c.send(response.encode())

    elif "POST" in request:
        data = request.split("\n\n")[1]

        f = open("upload.txt","w")
        f.write(data)
        f.close()

        c.send("HTTP/1.1 200 OK\n\nFile Uploaded".encode())

    c.close()
```
CLIENT:
```
import socket

s = socket.socket()
s.connect(("localhost",3024))

ch = input("1.Download 2.Upload : ")

if ch == "1":
    req = "GET / HTTP/1.1\nHost: localhost\n\n"
    s.send(req.encode())

    data = s.recv(4096)
    print(data.decode())

else:
    msg = input("Enter data to upload: ")

    req = "POST / HTTP/1.1\nHost: localhost\n\n" + msg
    s.send(req.encode())

    data = s.recv(1024)
    print(data.decode())

s.close()
```
UPLOADED FILE:
```
req = "POST / HTTP/1.1\nHost: localhost\n\n" + msg
s.send(req.encode())

data = s.recv(1024)
print(data.decode())
```
## OUTPUT
<img width="936" height="175" alt="Screenshot 2026-05-26 164533" src="https://github.com/user-attachments/assets/0aff86e0-70c7-47be-aeaf-c3b92c90de52" />
<img width="933" height="150" alt="Screenshot 2026-05-26 164541" src="https://github.com/user-attachments/assets/930b1b70-aaed-4a2b-8ead-ff0f55671b04" />
<img width="448" height="210" alt="Screenshot 2026-05-26 164547" src="https://github.com/user-attachments/assets/2d3e3c35-c57b-4330-9d39-58ce41824544" />

## Result
Thus the socket for HTTP for web page upload and download created and Executed
