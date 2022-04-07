# go_Web
Go web learning note

# demo
配置简单的路由
```
  http.HandleFunc("/", sayhelloName)       //设置访问的路由
	err := http.ListenAndServe(":9090", nil) //设置监听的端口
```
