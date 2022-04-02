# 处理文件上传
通过上面的代码可以看到，处理文件上传我们需要调用
```r.ParseMultipartForm```，里面的参数表示maxMemory，
调用```ParseMultipartForm```之后，
上传的文件存储在maxMemory大小的内存里面，
如果文件大小超过了maxMemory，那么剩下的部分将存储在系统的临时文件中。
我们可以通过```r.FormFile```获取上面的文件句柄，然后实例中使用了io.Copy来存储文件。
