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
```python
import socket

def send_request(host, port, request):
    with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
        s.connect((host, port))
        s.sendall(request.encode())
        response = b""
        while True:
            data = s.recv(4096)
            if not data:
                break
            response += data
    return response

def download_file(host, port, filename):
    request = f"GET /{filename} HTTP/1.1\r\nHost: {host}\r\nConnection: close\r\n\r\n"
    response = send_request(host, port, request)

    headers, _, body = response.partition(b"\r\n\r\n")
    with open("downloaded_" + filename, "wb") as f:
        f.write(body)
    print(f"✅ File '{filename}' downloaded successfully as 'downloaded_{filename}'")

if __name__ == "__main__":
    host = "127.0.0.1" 
    port = 8080
    filename = "example.txt"

    download_file(host, port, filename)
```
## OUTPUT
<img width="2880" height="1800" alt="image" src="https://github.com/user-attachments/assets/f44e8392-05a8-45a0-b339-11aecffff357" />

## Result
Thus the socket for HTTP for web page upload and download created and Executed
