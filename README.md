# 5a_Create_Socket_for_HTTP_for_webpage_upload_and_download
## AIM :
To write a PYTHON program for socket for HTTP for web page upload and download

## Date: 11/03/2026
## Roll.No: 212225040323

## Algorithm

1. Start the program.

2. Create a socket using Python socket library.

3. Bind the socket to localhost and port 8080.

4. Listen and accept connection from the client.

5. Receive HTTP request from the client.

6. If the request is GET, read the webpage file and send it to the client.

7. If the request is POST, receive the uploaded data and store it in a file.

8. Send HTTP response to the client.

9. Close the connection.

10. Stop the program.

## Program 

httpserver.py

```
import socket

s = socket.socket()
s.bind(("localhost",8080))
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

httpclient.py

```
    import socket

s = socket.socket()
s.connect(("localhost",8080))

ch = input("1.Download 2.Upload : ")

# Download webpage
if ch == "1":
    req = "GET / HTTP/1.1\nHost: localhost\n\n"
    s.send(req.encode())

    data = s.recv(4096)
    print(data.decode())

# Upload file
else:
    msg = input("Enter data to upload: ")

    req = "POST / HTTP/1.1\nHost: localhost\n\n" + msg
    s.send(req.encode())

    data = s.recv(1024)
    print(data.decode())

s.close()
```

## OUTPUT

### 1. DOWNLOAD

Server-Side

![alt text](<Screenshot 2026-03-11 112937.png>)

Client-Side

![alt text](<Screenshot 2026-03-11 112958.png>)

Execution

![alt text](<Screenshot 2026-03-11 112852.png>)

### 2. UPLOAD

Server-Side

![alt text](<Screenshot 2026-03-11 113104.png>)

Client-Side

![alt text](<Screenshot 2026-03-11 113124.png>)

Execution

![alt text](<Screenshot 2026-03-11 113047.png>)

## Result
Thus the socket for HTTP for web page upload and download created and Executed
