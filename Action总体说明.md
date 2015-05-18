# 设计定位
1. Action表达的是一个执行过程，可以运行一段时间。典型的Action包含3个函数Enter、Execute、Exit，简称3E

# 公共参数
##### life-circle(生命周期)
1. work(默认值)
> work表示以Action的工作周期为生命周期

2. passive
3. endless
4. passive-work
5. duration

##### duration(工作周期)
> 用一个固定的值设置Action的工作周期，如果life-circie没有设置，或者设置为diration, 这个字段设置的工作周期都能起效果，如果life-circle设置了，并且是其他值，则直接报错

##### work
> 当Action启动时候，给Action发送一个事件，这个事件只有Action注册的事件处理函数才能处理，对Action外部没有任何影响

##### convert
> 给Action自动注册一个事件转换器，在整个Action的生命周期中工作，当接收到一个事件以后，转换为另外一个事件给Action使用，转换后的事件只有在这个Action中注册的事件处理函数才能处理，对Action外部没有任何影响

# 一下是一些预先定义好的模块， 提供了一些预先实现好的Action
1. [Chipmunk模块](module_chipmunk)