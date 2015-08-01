#### 脚本

脚本缩进错误，请勿直接拷贝

	 - ui-play-anim:
     control: MenuMainBarPage.VipAnim_panel
     back_res: 'Ui/Spine/Menu/UI_icon_vip.spine#icon_v0'

##### ui-play-anim:
action名称，意思为，播放动画。
此action支持播放Spine动画和Particle

##### control
控件名称。
MenuMainBarPage为Page的名称
VipAnim_panel为Page中使用的控件名称。

##### back_res
背景资源，其实就是要在control上播放的动画资源
为啥叫back_res呢，因为在UI控件上有个接口叫setBackFrame
即背景显示资源。这里用back_res，或许还有force_res吧

	'Ui/Spine/Menu/UI_icon_vip.spine#icon_v0'
    
中，

	Ui/Spine/Menu/UI_icon_vip.spine
    
表示使用的Spine资源文件名。

	#icon_v0

为该Spine中animation的名称。

	 back_res: 'Ui/Spine/Menu/UI_icon_vip.spine#icon_v0'
     
也支持这样写

	 back_res: 'Ui/Spine/Menu/UI_icon_vip.spine#icon_v0*1+icon_v1'
     
意思为名称为icon_v0的animation播放一次之后，播放icon_v1无数次。