# 设计定位
1. Action表达的是一个执行过程，可以运行一段时间。典型的Action包含3个函数Enter、Execute、Exit，简称3E

# 公共参数
##### name
> 给Action一个名字，在同一个State下面，名字不能重复。
名字的唯一作用就是给其他Action在设置follow参数时指定，唯一标志同一个State下的Action。
设置名字以后有一个附带的好处，就是日志中可以看到对应的输出，比较容易定位问题，可以考虑在定位问题时设置一个不常用的奇怪名字进行标识，定位完成删除

##### follow
> 设定Action的依赖关系，只有依赖的Action完成以后，当前的Action才会开始工作

##### life-circle(生命周期)
1. work(默认值)
> work表示以Action的工作周期为生命周期。
启动Action以后，如果没有update函数，或者update函数停止，则认为Action生命周期结束。
在整个Action的update 执行过程中，都认为是在工作。

2. passive
> passive表示这个Action不计算在State的活动Action中，同时也不会认为是停止工作。
Action一旦启动，就会一直到State停止才会调用Exit，无论update函数是否在工作。
和endless的唯一区别是是否计算在State的工作状态中。

3. endless
> endless表示Action一旦启动，无论update函数是否工作，都不会结束工作

4. passive-work
5. duration
> 设置一个Action的工作事件，这个选项一般不直接使用，而是通过duration参数隐含使用

##### duration(工作周期)
> 用一个固定的值设置Action的工作周期，如果life-circie没有设置，或者设置为diration, 这个字段设置的工作周期都能起效果，如果life-circle设置了，并且是其他值，则直接报错

##### work
> 当Action启动时候，给Action发送一个事件，这个事件只有Action注册的事件处理函数才能处理，对Action外部没有任何影响

##### convert
> 给Action自动注册一个事件转换器，在整个Action的生命周期中工作，当接收到一个事件以后，转换为另外一个事件给Action使用，转换后的事件只有在这个Action中注册的事件处理函数才能处理，对Action外部没有任何影响

# 重要的Action提供模块
1. [[Animation模块]]
1. [[2DTransform模块]]
1. [[Chipmunk模块]]