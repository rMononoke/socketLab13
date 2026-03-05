# 2c

## A: TCP echo client

```python
import socket
sock = socket.socket()            # (1) Создать TCP-сокет
sock.connect(('localhost', 9090)) # (2) Подключиться к серверу
sock.send(b"hello")               # (3) Отправить байты
data = sock.recv(1024)            # (4) Принять (макс. байт)
sock.close()                      # (5) Закрыть сокет
print(data.decode())              # (6) bytes -> string
``` 

## B:

```python
import socket
sock = socket.socket()
sock.bind(('', 9090))
sock.listen(1)
print("server listening")
while True:                      # (1) Бесконечный цикл
    conn, addr = sock.accept()   # (2) Ожидать клиента
    print("client", addr)
    data = conn.recv(1024)
    conn.send(data)
    conn.close()                 # (3) Закрыть соединение (не sock)
print("done")
```

## C:

```python
import socket
sock = socket.socket(socket.AF_INET, socket.SOCK_DGRAM) # (1) UDP-сокет
sock.sendto(b"hello udp", ('localhost', 9091))          # (2) Отправить по (хост, порт)
data, addr = sock.recvfrom(1024)                        # (3) Принять
print("echo", data.decode())
sock.close()
```

## D:

```python
import socket

sock = socket.socket()
sock.connect(('localhost', 9090))
msg = "hello"
sock.send(msg.encode())  # (1) string -> bytes
data = sock.recv(1024)
sock.close()
print(data.decode())     # (2) bytes -> string
```
