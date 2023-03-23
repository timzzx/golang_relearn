# go slice

slice 和 slice 指针有什么区别
> slice 其实是一个结构体，包含len,cap,array
> 不管传的是 slice 还是 slice 指针，如果改变了 slice 底层数组的数据，会反应到实参 slice 的底层数据。