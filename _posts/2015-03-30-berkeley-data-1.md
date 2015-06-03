---

layout: post

title: "Berkeley CS 61B 1, Start"

categories: jekyll update 

---

## Java Content

1. Static 

	每个Class只有一份。比如NumberOfPeople这样的变量。
同时method也可以是static的。都直接可以从Class来调用。不需要特定的Object。

2. final

final的含义是一旦定义，那么不再能够修改。

变量：如果是primative variable，那么赋值以后不能修改。如果是object或者array，那么内容刻意修改，但是不能修改指向别的object或者array。

方法：不能被重写

类：不能被继承