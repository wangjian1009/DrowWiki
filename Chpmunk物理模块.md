#### 基本概念

#### 环境相关的配置
Entity系统需要使用物理模块首先必须在场景定义文件中加载物理运行的环境，一般配置文件路径在
etc/scene/scene.yml
>   - ChipmunkEnv:
>      debug: 1
>      debug-layer: debug
>      update-priority: -1
>      step-duration: 0.01
>      mask:
>        \- type1
>        \- type2

配置项的详细说明
1. *update-priority* 用于控制更新的顺序，物理引擎一般配置为负数，确保在其他模块（如绘制）更新前处理
2. *step-duration* 迭代间隔，独立于刷新间隔，确保物理引擎的表现一致。
3. *mask* 一个物理对象分类的定义，方便配置中使用字符串表示对象类型

#### 物体类型定义
1. *static* 静止的物体，引擎不会根据速度更新其位置
2. *kinematic* 运动的物体，引擎会根据速度更新其位置，但是不会处理加速度（如系统的重力，附加的加速度）
3. *dynamic* 动态的物体，引擎会根据加速度，力等更新其位置。

#### 运行模式定义
1. *active* 物理层的位置信息更新到逻辑层，由物理层控制对象运动
2. *passive* 逻辑层的位置信息更新到物理层，由逻辑层控制对象的运动

#### 形状定义格式
1. box: lt.x=0.0f, lt.y=0.0f, rb.x=1.0f, rb.y=1.0f
2. circle: radius=1.0f, center.x=0.0f, center.y=0.0f
3. entity-rect: adj.x=0.0f, adj.y=0.0f
4. sector: center.x=0.0f, center.y=0.0f, radius=1.0f, angle-start=0.0f, angle-range=0.0f, angle-step=0.0f