# Go如何使得Web工作

# web工作方式的几个概念

```Request：用户请求的信息，用来解析用户的请求信息，包括post、get、cookie、url等信息

Response：服务器需要反馈给客户端的信息

Conn：用户的每次请求链接

Handler：处理请求和生成返回信息的处理逻辑
```

# http包执行流程

```
创建Listen Socket, 监听指定的端口, 等待客户端请求到来。

Listen Socket接受客户端的请求, 得到Client Socket, 接下来通过Client Socket与客户端通信。

处理客户端的请求, 首先从Client Socket读取HTTP请求的协议头, 如果是POST方法, 还可能要读取客户端提交的数据, 
然后交给相应的handler处理请求, handler处理完毕准备好客户端需要的数据, 通过Client Socket写给客户端。
```

