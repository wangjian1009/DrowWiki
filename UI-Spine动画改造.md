### 原因
因为历史原因，UI Page在调度时，脚本分为_enter,_back，和正常显示三部分。为了保证在这几种情况下，Spine Object的生命周期均有效，所以把Spine Object的初始化和Controls的绑定放在了 _init文件中。_init在Main中调用，从而保证其生命周期始终有效。
一些公共的Spine Object，放在common目录下。一些比较特殊的公共部分，比如部分Page的背景为通用Spine动画，但是又需要绑定关闭按钮，这种情况的做法会在下边详细说明。

### _init.yml
该