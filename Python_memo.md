###  namespace
Python中通过提供 namespace 来实现重名函数/方法、变量等信息的识别，其一共有三种 namespace，分别为：

* local namespace: 作用范围为当前函数或者类方法
* global namespace: 作用范围为当前模块
* build-in namespace: 作用范围为所有模块

当函数/方法、变量等信息发生重名时，Python会按照 “local namespace -> global namespace -> build-in namespace”的顺序搜索用户所需元素，并且以第一个找到此元素的 namespace 为准。

同时，Python中的内建函数locals()和globals()可以用来查看不同namespace中定义的元素。

Python中怎么创建闭包

在Python中创建一个闭包可以归结为以下三点：

* 闭包函数必须有内嵌函数
* 内嵌函数需要引用该嵌套函数上一级namespace中的变量
* 闭包函数必须返回内嵌函数

例子如下

    def greeting_conf(prefix):
        def greeting(name):
            print(prefix, name)
        return greeting

### 判断字符编码

使用chardet包判断字符编码类型，只能`判断是否为某种编码的概率`,输入参数类型为str。

    import chardet
    with open('file','rb')as f:
        guess=chardet.detect(f.read())
    print(guess)
    //{'language: 'Japanese','confidence': 0.99, 'encoding': 'SHIFT_JIS'}
