##多文件方式实现进入退出
###以抽奖lottery为例：
####1.控件之间的跳转定义
定义位置： FlightRes\flight_res\Ui\Spine\State\UI_lottery_1.spine-state
定义方法：
#####a．名字定义
```javascript
  main:
  init_state: hide
  states:
    - name: hide
      anim: empty_1  
      
    - name: Buy_1_down
      anim: idle_1_down_l
```
对应于spine动画的每个名字所有animations均需要定义，相互对应。
#####b．状态定义
```javascript
transitions:
    - from: hide
      to: show
      anim: appear_1
      name: show
      
    - from: show
      to: hide
      anim: disappear_1
      name: hide
```
from：名字
to： 名字
anim：过度状态
name：命名  名字可重复
一般为from不同的命名可重复
####2.spine的初始化定义
定义位置： FlightRes\flight_res\runtime\ui\phases\Menu\spine-init\Lottery_init.yml
#####定义方法：
```javascript
init-state: Init
Init:
  Actions: 
     - spine-with-obj:
        life-circle: passive
        obj-name: SpineLottery_1
        obj-res: Ui/Spine/Menu/UI_gacha_1.spine
        obj-state-def: Ui/Spine/State/UI_lottery_1
```
-  spine-with-obj：定义Spine的obj
life-circle：passive生存周期为被动（区别于endless）
obj-name：obj命名（定义之后只需使用.main即可调用Spine的动画）
obj-state-def：spine控件所使用的跳转定义

#####将UI控件与spine绑定
```javascript
    - spine-ui-bind-controls:
         debug: 1
         life-circle: passive
         obj-name: SpineLottery_1
         root-control: MenuLotteryPage
         prefix: ctrl1_
```
debug： 1  可用于显示UI与spine的绑定结果，成功显示ok，失败显示ignor
 obj-name：命名的obj名字
 root-control：控制页位于FlightRes\flight_res\runtime\ui\pages\
 prefix：ctrl_ 根据名字匹配相应控制触发器
 
```javascript
    - ui-play-anim:
        life-circle: passive
        control: MenuLotteryPage.ByMoneySpine_panel
        back_res: '[name=SpineLottery_1]'
```
 control：控制panel位于UI内的特定panel（此绑定panel不能作为已绑定的子控件的父类）
 back_res：’[name=obj-name]’操作之后的返回资源
####3.enter动画
位置： FlightRes\flight_res\runtime\ui\common\fsm\Lottery_enter.yml
#####隐藏当前page方法：
```javascript
Actions:
  - run-fsm:
      name: hide-old
      fsm:
        init-state: Do
        Do:
          Actions:
            - run-fsm:
                life-circle: passive
                fsm:
                  import: ui.common.fsm.Show-Background

            - run-fsm:
                fsm:
                  import: ui.common.fsm.MainTail_back
```
隐藏之前的页面，对于Lottery来说就是主页面隐藏
import背景图之后退出主界面
#####显示抽奖page方法：
```javascript
- run-fsm:
      follow: hide-old
      name: show-in-anim
      fsm:
        init-state: Do
        Do:
          Actions:
            - run-fsm:
                life-circle: passive
                fsm:
                  import: ui.common.fsm.Show-BK-With-HB_enter
```
#####调用抽奖spine动画方法：
```javascript
- spine-apply-transition:
        part: SpineLottery_1.main
        transition: show
```
transition:表示跳转定义的动画方法show为显示动画的名字
####4.back动画
位置： FlightRes\flight_res\runtime\ui\common\fsm\ Lottery _back.yml
#####隐藏当前抽奖页面方法：
```javascript
Actions:
  - run-fsm:
      name: hide-old
      fsm:
        init-state: Do
        Do:
          Actions:
            - run-fsm:
                life-circle: passive
                fsm:
                  import: ui.common.fsm.Show-BK-With-HB_back

            - ui-show-page:
                life-circle: passive
                page: MenuLotteryPage
                before-page: MenuFootPage

            - spine-apply-transition:
                part: SpineLottery_1.main
                transition: hide 
```
与enter原理相同，先要将lottery页面隐藏，之后显示所要返回的page
```javascript
- run-fsm:
      follow: hide-old
      fsm:
        init-state: Do
        Do:
          Actions:
            - run-fsm:
                fsm:
                  import: ui.common.fsm.MainTail_enter
```
####5.显示page的设定
位置：FlightRes\flight_res\runtime\ui\common\fsm\ Lottery.yml
#####方法：
```javascript
Actions:
  - run-fsm:
      life-circle: passive
      fsm:
        import: ui.common.fsm.Show-BK-With-Handbook

  - ui-show-page:
      page: MenuLotteryPage
      before-page: MenuFootPage

  - run-fsm:
      life-circle: passive
      fsm:
        import: ui.common.fsm.Show-Foot
```
在抽奖page内将会用到的页要在action中指定

```javascript
Navigations:
  - trigger: MenuFootPage.Cancel_button
    back:

  - trigger: MenuFootPage.Note_button
    call-to: Handbook
    enter: Handbook_enter
    leave: Handbook_back
    suspend: 0

  - trigger: MenuLotteryPage.MoneyTen_button
    call-to: LotteryResult
    suspend: 0

  - trigger: MenuLotteryPage.MoneyOne_button
    call-to: LotteryResult
    suspend: 0
```
对page内的操作进行处理，设定button的处理脚本
####6.在main.yml中添加的page的init脚本
```javascript
- run-fsm:
      life-circle: passive
      fsm:
        import: ui.phases.Menu.spine-init.LevelEndless_init
```
将之前写好的init.yml文件在main.yml中进行定义
```javascript
- trigger: MenuMainPage.Endless_button
    call-to: End
    enter: LevelEndless_enter
    leave: LevelEndless_back
    suspend: 1
```
由于抽奖page是在主界面上，所以要对抽奖的button进行处理，设定呼出的页面以及进入页和离开页，
suspend表示停留时间