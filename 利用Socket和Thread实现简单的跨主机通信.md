##  Socket 和 Thread

### Scoket

socket (套接字) 是不同主机间的进程通信通信方式,TCP/UDP 是 socket 两种主要的通信方式.

### Thread

Thread(线程) 线程是操作系统的执行单元,线程属于进程,每个进程下面至少有一个线程.

## 通过 socket 创建 UDP 连接

相比于 TCP, UDP 是一种面向无连接的协议,在知道对方的 IP 地址和端口后就能发送数据,但是对方能不能收到 UDP 不知道,但是 UDP 的优点是快.

一个完整的 UDP 连接包含客户端和服务端,如果想要实现客户端和服务端之间相互通信,那么客户端端与服务端都需要实现信息的接收与发送.

* 创建 UDP 服务端

```python
# 导入 socket 包
import socket
# 创建连接
# AF_INET: INTERNET 通信
# SOCK_DGRAM: 以数据报形式传递
udp_server = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
# 创建连接后,需要指定接收信息的 IP 和端口
# socket 用 bind 方法绑定 IP 和端口
# 注意: bind 接收的是一个元祖
# '' 表示使用当前主机 IP
server_addr = ('', 8080)
socket_test.bind(server_addr)
# 绑定端口后就可以接收来自其他主机的信息了
# recvfrom 中参数是指定接收数据大小
# 如果没有数据发送过来会一直等待,不会执行后面程序
# 它会返回两个值,一个是客户端发送过来的信息,一个是客户端 IP 和端口
recv_data, client_addr = udp_server.recvfrom(1024)
# 如果想显示数据可以 print
# decode 是对数据进行解码,用什么格式编码就用什么格式解码
print(recv_data.decode('utf-8'))

# 如果想实现信息的发送功能
# 可以通过 sendto 方法
# sendto 第一个参数是需要发送的信息 第二个参数是对方 IP 和端口
send_data = 'hi'
udp_server.sendto(send_data.encode('utf-8'), client_addr) 
# 最后需要关闭 socket 连接
udp_server.close()
```

完整代码

```python
#!/usr/bin/env python3

import socket

def udpServer(udp_server, recv_addr):
    udp_server.bind(recv_addr)
    recv_data, client_addr = udp_server.recvfrom(1024)
    print('接收到来自<%s>的信息' % client_addr[0],
          recv_data.decode('utf-8'))
    
    send_data = input('发送信息:')
    udp_server.sendto(send_data.encode('utf-8'), client_addr)
    udp_server.close()
   
if __name__ == '__main__':
    udp_server = socket.socket(socket.AF_INET,
                               socket.SOCK_DGRAM)
    recv_ip = input('接收信息 IP, 不输入默认本机:')
    recv_port = int(input('接受信息端口:'))
   	recv_addr = (recv_ip, recv_port)
    
    udpServer(udp_server, recv_addr)

```

UDP 客户端和服务端基本一样,只是服务端是先接收后发送,而客户端是先发送后接收.

* 客户端

```python\
#!/usr/bin/env python3

import socket

def udpClient(udp_client, send_addr, recv_addr):
	send_data = input('发送信息:')
	udp_client.sendto(send_data.encode('utf-8'), send_addr)	

	udp_client.bind(recv_addr)
	recv_data, server_addr = udp_client.recvfrom(1024)
	print('接收到来自<%s>的信息' % server_addr[0],
          recv_data.decode('utf-8'))
    
	udp_client.close()
   
if __name__ == '__main__':
    udp_client = socket.socket(socket.AF_INET,
                               socket.SOCK_DGRAM)
    send_ip = input('服务端 IP:')
    send_port = input('服务端端口:')
    recv_ip = input('接收信息 IP, 不输入默认本机:')
    recv_port = int(input('接受信息端口:'))
   	send_addr = (send_ip, send_port)
   	recv_addr = (recv_ip, recv_port)
    
    udpClient(udp_client, send_addr)
```

当两个文件都启动时,就可以进行通信了,但是这样只能先由客服端发送信息,并且只能通信一次.如果想进行连续的通信,那么可以通过循环来实现,但是还是只能先接收后发送或者先发送后接收,因为 `recvfrom()` 方法在没有接收信息时会造成堵塞,让程序无法继续运行.

## 通过多线程实现类 QQ 通信

Python 通过 `threading` 包实现多线程

```python
# 导入 threading 包
import threading
import time

def write():
    for i in range(5):
        print('写代码')
        time.sleep(0.5)
        
def listen():
    for i in range(5):
        print('听歌')
        time.sleep(0.5)

if __name__ == '__main__':
    # 创建线程
    thread1 = threading.Thread(target=write)
    thread2 = threading.Thread(target=listen)
    
    # 开始
    thread1.start()
    thread2.start()

# 输出
//写代码
//听歌
//休眠一秒
//写代码
//听歌
//休眠一秒
//写代码
//听歌
//休眠一秒
```

上面代码是线程创建, `write 和 listen`  会同时打印.可以解决 UDP 通信时堵塞问题,让接收和发送运行在不同的线程上.

### 线程和 socket 结合

使用多线程后就不需要处理谁先接收和谁先发送,因为接收和发送存在与不同的线程中.所以服务端和客户端的代码可以一样

```python
#!/usr/bin/env python3

import socket
import threading
import os, signal

def udp_socket_recv_client(udp_socket_client, recv_address):
    udp_socket_client.bind(recv_address)
    while True:
        recv_data, recv_addr = udp_socket_client.recvfrom(1024)
        print('\n')
        print('>> [收到來自<%s>的信息啦]'% recv_addr[0],
                recv_data.decode('utf-8') + '\n' + '<<', end='')

def udp_socket_send_client(udp_socket_client, send_address):
    print('鏈接成功,可以發送信息了:)')
    while True:
        send_data = input('<<')
        # 退出程序
        if send_data == 'QUIT':
            udp_socket_client.close()
            print('退出成功')
            os.kill(os.getpid(), signal.SIGKILL)
        else:
udp_socket_client.sendto(send_data.encode('utf-8'), send_address)

def main():
    udp_socket_client = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
	
    # 自定义接收和发送 IP 和 port
    print('輸入 QUIT 退出程序')
    recv_ip = input('接受信息 IP 不輸入默認本機 IP:')
    recv_port = input('接受信息端口:')
    send_ip = input('對方 IP:')
    send_port = input('對方接受信息端口:')
    recv_address = (recv_ip, int(recv_port))
    send_address = (send_ip, int(send_port))

    socket_send_thread = threading.Thread(target=udp_socket_send_client,
            args=(udp_socket_client, send_address)
            )
    socket_recv_thread = threading.Thread(target=udp_socket_recv_client,
            args=(udp_socket_client, recv_address)
            )
    socket_recv_thread.start()
    socket_send_thread.start()

if __name__ == '__main__':
    main()

```

运行结果:

![](C:\Users\Administrator\Desktop\UDP通信.png)