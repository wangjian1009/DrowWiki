##关于Page##
详见: [[Page]]

##制作UI资源##
使用REditor制作UI资源，将界面中添加需要的控件然后命名、放好位置。制作好之后保存，并运行资源打包脚本，将资源导出。

##增加Page类##
增加相应的Page cpp文件。编辑代码，实现需要实现的功能。
详见： [[Page类说明]]

##增加关联配置##
关联配置为Page类与UI资源相关联的配置文件。

示例代码：
<code>
load-from: Ui/Menu/Shop.lay.bin
phases: [ Menu ]
</code>

一般关联文件内容都为两行。
1. 第一行为所需UI资源的路径及名称。为.bin是因为资源在执行打包脚本后为.bin文件。
2. 第二行为...应该是目录吧

##修改symbols##
此文件FlightCli\game目录下
应该是两个文件，一个是vc工程使用，一个是xcode使用
当编辑该文件时，需要修改两个文件，将内容添加进去。

symbols.vc.def内添加的内容为：
<code>
Page类名称_app_init
Page类名称_app_fini
</code>

symbols.def内添加的内容为：
<code>
_Page类名称_app_init
_Page类名称_app_fini
</code>

symbols.def