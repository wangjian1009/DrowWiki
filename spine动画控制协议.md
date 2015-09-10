# Spine控制单个Particle文件中的多个发射器
##### 名字匹配规则
	Spine定义Slot和Particle文件中的发射器名字匹配，
    通过统一前缀定义Slot的名字，一般建议用 PE_ 开头
    如 PE_fire_1 对应Particle文件中的 fire_1_a, fire_1_b
##### 参数定义
	Slot的名字可以通过方括号形式向发射器传递参数，例如
   	PE_fire_1[rotate=1] 继续匹配file_1_a，file_1_b, 并且这两个发射器接受骨骼旋转的控制。

##### 支持的参数列表
1. rotate
	发射器是否接受骨骼的旋转控制，取值 1,0, 默认值0
1. flip
	发射器是否接受骨骼的镜像控制，取值 1,0, 默认值0
1. scale
	发射器是否接受骨骼的缩放控制，取值 1,0, 默认值0
1. rotate-adj
	附加的旋转角度，无论是否支持骨骼选择的控制，都会叠加这个旋转到发射器

##### 控制发射器的发射
    绑定的Slot一点显示，则代表发射器开启，关闭，则对应的发射器关闭（停止发射关闭）
    对于Passive的发射器，每次打开都相当于一次触发，关闭没有意义，只是为了下一次打开

##### 其他说明
1. 目前Particle的文件名指定还在脚本中指定
1. 发射器的位置是Slot所属的骨骼定义的
1. 匹配通过Slot的名字进行，Slot所属骨骼的名字没有关系

##### 相关Action
1. Spine骨骼绑定Part [spine-bind-part](/Spine-Actions)
1. Particle的发射器接收Part控制 [particle-emitter-bind-part](/Particle-Actions)

---------------------------------------
# Spine定义碰撞框