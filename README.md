

# File-transfer-project

# 📁 Python TCP File Transfer System

This project implements a simple **client-server file transfer system** using **Python sockets** over **TCP/IP**. The client sends a file to the server, which receives and stores it.

---

## 🧩 Project Structure

```
.
├── client.py       # Client-side script to send a file
├── server.py       # Server-side script to receive a file
└── README.md       # Documentation
```

---

## 🚀 How It Works

### ✅ Server Side (`server.py`)

* Listens on a specified port (default: 5001)
* Accepts incoming client connection
* Receives file data in 4096-byte chunks
* Saves it as `received_file.txt`

### ✅ Client Side (`client.py`)

* Connects to the server via IP and port
* Opens the selected file in binary mode
* Sends the file in 4096-byte chunks
* Closes the connection after completion

---

## ⚙️ Requirements

* Python 3.x
* No external libraries needed

---

## ▶️ Usage

### 1. Run the Server

Open Terminal 1:

```bash
python server.py
```

Output:

```
SERVER WAITING FOR CONNECTION...
CONNECTED BY ('127.0.0.1', <port>)
FILE RECEIVED AND SERVER CLOSED.
```

### 2. Run the Client

Open Terminal 2:

```bash
python client.py
```

Output:

```
CLIENT STARTED
CLIENT STOPPED
```

---

## 🧠 Customization

* Change `file_path` in `client.py` to send a different file.
* Modify `filename` in `server.py` to store under a new name.
* Adjust `host`, `port`, or `buffer_size` as needed in both scripts.

---

## 📜 Example Code Summary

### 🔹 `client.py`

```python
import socket

def send_file(file_path, host='127.0.0.1', port=5001, buffer_size=4096):
    client_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    client_socket.connect((host, port))
    print("CLIENT STARTED")

    with open(file_path, 'rb') as f:
        while True:
            bytes_read = f.read(buffer_size)
            if not bytes_read:
                break
            client_socket.sendall(bytes_read)

    client_socket.close()
    print("CLIENT STOPPED")

if __name__ == "__main__":
    send_file("file.txt")
```

### 🔹 `server.py`

```python
import socket

def start_serve(host='0.0.0.0', port=5001, filename="received_file.txt", buffer_size=4096):
    server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    server_socket.bind((host, port))
    server_socket.listen(5)

    print("SERVER WAITING FOR CONNECTION...")

    conn, addr = server_socket.accept()
    print(f"CONNECTED BY {addr}")

    with open(filename, 'wb') as f:
        while True:
            bytes_read = conn.recv(buffer_size)
            if not bytes_read:
                break
            f.write(bytes_read)

    conn.close()
    server_socket.close()
    print("FILE RECEIVED AND SERVER CLOSED.")

if __name__ == "__main__":
    start_serve()
```

---

## 📌 Notes

* Make sure both scripts use the **same port and buffer size**.
* Run both scripts on the same machine or configure IP for remote transfers.

---

## ✅ Output Sample

```
> Server:
SERVER WAITING FOR CONNECTION...
CONNECTED BY ('127.0.0.1', 52698)
FILE RECEIVED AND SERVER CLOSED.

> Client:
CLIENT STARTED
CLIENT STOPPED
```

---

## 👨‍💻 Author

**Makeswaran K**
*ECE Engineer*

---

