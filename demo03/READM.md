# 验证表单的输入

# 必填字段

想要确保从一个表单元素中得到一个值，例如前面小节里面的用户名，
Go有一个内置函数len可以获取字符串的长度，
这样我们就可以通过len来获取数据的长度，例如：
```go
if len(r.Form["username"][0])==0{
    //为空的处理
}
```
```r.Form```对不同类型的表单元素的留空有不同的处理， 对于空文本框、空文本区域以及文件上传，元素的值为空值,而如果是未选中的复选框和单选按钮，则根本不会在r.Form中产生相应条目，如果我们用上面例子中的方式去获取数据时程序就会报错.

# 数字
要确保一个表单输入框中获取的只能是数字，例如，想通过表单获取某个人的具体年龄是50岁还是10岁，而不是像“一把年纪了”或“年轻着呢”这种描述。

```go

getint,err:=strconv.Atoi(r.Form.Get("age"))
if err!=nil{
    //数字转化出错了，那么可能就不是数字
}
//接下来就可以判断这个数字的大小范围了
if getint >100 {
    //太大了
}
```
或者：
```go
if m, _ := regexp.MatchString("^[0-9]+$", r.Form.Get("age")); !m {
    return false
}
```

# 中文
想通过表单元素获取一个用户的中文名字，但是又为了保证获取的是正确的中文，我们需要进行验证，而不是用户随便的一些输入。

```unicode``` 包下的```func Is(rangeTab *RangeTable, r rune) bool```进行判断

```go

if m, _ := regexp.MatchString("^\\p{Han}+$", r.Form.Get("realname")); !m {
    return false
}
```

# 英文
通过表单元素获取一个英文值，例如我们想知道一个用户的英文名，应该是astaxie，而不是asta谢。

```go

if m, _ := regexp.MatchString("^[a-zA-Z]+$", r.Form.Get("engname")); !m {
    return false
}
```
 
# 电子邮箱

```go

if m, _ := regexp.MatchString(`^([\w\.\_]{2,10})@(\w{1,}).([a-z]{2,4})$`, r.Form.Get("email")); !m {
fmt.Println("no")
}else{
fmt.Println("yes")
}
```

# 手机号码

```go

if m, _ := regexp.MatchString(`^(1[3|4|5|8][0-9]\d{4,8})$`, r.Form.Get("mobile")); !m {
return false
}
```

# 下拉菜单

<select>元素生成的下拉菜单中是否有被选中的项目。
有些时候黑客可能会伪造这个下拉菜单不存在的值发送给你，那么如何判断这个值是否是我们预设的值呢？



```html

<select name="fruit">
<option value="apple">apple</option>
<option value="pear">pear</option>
<option value="banana">banana</option>
</select>
```
```go

slice:=[]string{"apple","pear","banana"}
v := r.Form.Get("fruit")
for _, item := range slice {
    if item == v {
        return true
    }
}
return false
```

