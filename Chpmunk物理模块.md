#### 基本概念

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