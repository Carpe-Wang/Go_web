# go_Web
Go web learning note

# demo
配置简单的路由
```
  http.HandleFunc("/", sayhelloName)       //设置访问的路由
  err := http.ListenAndServe(":9090", nil) //设置监听的端口
```
在请求到localhost:9090/，地址的时候，会进入到相关的sayhelloName方法里面:
```
func sayhelloName(w http.ResponseWriter, r *http.Request) {
	r.ParseForm()       //解析参数，默认是不会解析的
	fmt.Println(r.Form) //这些信息是输出到服务器端的打印信息
	fmt.Println("path：", r.URL.Path)
	fmt.Println("scheme：", r.URL.Scheme)
	fmt.Println(r.Form["url_long"])
	for k, v := range r.Form {
		fmt.Println("key:", k)
		fmt.Println("val:", strings.Join(v, ""))
	}
	fmt.Fprintf(w, "Hello Carpe-Wang!") //这个写入到w的是输出到客户端的
}
```

其中方法中的```w http.ResponseWriter, r *http.Request```

w：服务器端需要传输给客户的相关信息写入

r：客户端请求服务器携带的参数，如：请求类型(get,post,updata,delete)

进行我们所需要的业务逻辑。




# demo01


web工作方式的几个概念

```Request：用户请求的信息，用来解析用户的请求信息，包括post、get、cookie、url等信息

Response：服务器需要反馈给客户端的信息

Conn：用户的每次请求链接

Handler：处理请求和生成返回信息的处理逻辑
```

http包执行流程

```
创建Listen Socket, 监听指定的端口, 等待客户端请求到来。

Listen Socket接受客户端的请求, 得到Client Socket, 接下来通过Client Socket与客户端通信。

处理客户端的请求, 首先从Client Socket读取HTTP请求的协议头, 如果是POST方法, 还可能要读取客户端提交的数据, 
然后交给相应的handler处理请求, handler处理完毕准备好客户端需要的数据, 通过Client Socket写给客户端。
```
# demo02

相对于demo而言多了一个相对应的页面解析和处理不同的业务逻辑请求
```
func login(w http.ResponseWriter, r *http.Request) {
	fmt.Println("method:", r.Method) //获取请求的方法
	if r.Method == "GET" {
		t, _ := template.ParseFiles("login.gtpl")
		log.Println(t.Execute(w, nil))
	} else {
		//请求的是登录数据，那么执行登录的逻辑判断
		fmt.Println("username:", r.Form["username"])
		fmt.Println("password:", r.Form["password"])
	}
}
```
