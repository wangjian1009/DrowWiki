##说明##
Page即单个功能界面，比如充值界面。

##包含元素##
每个Page必须包含以下内容
1. Page类
1. UI资源
1. 关联配置

对应的目录为：
1. FlightCli\game\UI\Menu\
1. FlightRes\flight_res\Ui\Menu\
1. FlightRes\flight_res\runtime\ui\pages\

比如充值界面：
1. 类：MenuRechargePage.cpp
1. UI资源：Recharge.lay
1. 关联配置：MenuRechargePage.yml

UI资源必须使用REditor来编辑，具体信息见 [[UI工具]]