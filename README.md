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
	fmt.Fprintf(w, "Hello astaxie!") //这个写入到w的是输出到客户端的
}
```
进行我们所需要的业务逻辑。
