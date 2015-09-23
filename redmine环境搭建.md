1. 确认redmine版本以及依赖的ruby版本
1. 安装ruby（以redmine用户，独立从源代码安装）
1. 设置用户环境变量，以确保使用新安装的ruby
	\# vi ~/.bashrc
    export PATH=$HOME/bin:$PATH
	export MANPATH=$HOME/share/man:$MANPATH
	\# source ~/.bashrc #确保环境变量生效
    \# which ruby

1. RubyGems
	\# wget http://rubyforge.org/frs/download.php/60718/rubygems-1.3.5.tgz
	\# tar zxvf rubygems-1.3.5.tgz
	\# cd rubygems-1.3.5
	\# ruby setup.rb

1. 修改gem的安装源  [[RubyGem默认源安装太慢，修改国内淘宝源]]

1. Rake安装
	\# gem install rake

1. Ruby on Rails
	\# gem install rails

1. 下载redmine
	\# git clone https://github.com/redmine/redmine
    \# cd redmine
    \# git checkout 3.1-stable #版本需要确认

1. 修改redmine配置，从国内源下载所有依赖项目  [[RubyGem默认源安装太慢，修改国内淘宝源]]
	\# vi redmine/Gemfile 
    
1. 下载所有依赖
	\# cd redmine
    \# bundle update
如果有错误，根据错误提示安装依赖的系统包并重试这个过程
ubuntu上包括的包
	sudo apt-get install libmagickwand-dev
	
1. redmine数据库配置
	\# cd redmine/config
    \# #设置数据库参数
	\# cp database.yml.example database.yml
	\# vi database.yml
	production:
	adapter: mysql
	database:redmine
	host: localhost
	username: redmineuser
	password: redminepw
	encoding: utf8
	:wq
    
1. 创建mysql数据库 [[Mysql数据库-用户以及权限]]
	\# /usr/local/mysql/bin/mysql -u root -p
	Mysql> create database redmine default character set utf8;
	grant all on redmine.* to root;
	grant all on redmine.* to root@localhost;
	grant all on redmine.* to redmineuser;
	grant all on redmine.* to redmineuser @localhost;
	set password for redmineuser@localhost=password('redminpw');
	Mysql>exit;
    
1. Remine设定
	（注意此时的目录一定要在redmine/config里，不然会出错，本文后面有错误信息。）
	\# rake db:migrate RAILS_ENV="production" //创建表
	\# rake redmine:load_default_data RAILS_ENV="production" //加载默认配置
	这里会要求选择默认语言，我选的中文zh：
	Select language: bg, ca, cs, da, de, en, es, fi, fr, he, hu, it, ja, ko, lt, nl, no, pl, pt, pt-br, ro, ru, sk, sr, sv, th, tr, uk, vn, zh, zh-tw [en] zh
	这个默认设置只是在未登录时的界面语言，当用户登录后，默认语言还是英语，在My account里可以修改成其它语言。

1. 启动WEB服务
	\# ruby bin/rails server -e production -b '*'

1. 服务方式启动
	\# ruby bin/rails server -e production -b '*' -d
    
1. 服务方式停止
	（ps命令查出此进程的pid号，再杀掉，目前好像只能这样，我看了--help里面，还没有停止的参数。）
	\# ps aux | grep ruby
	\# kill -9 [PID]

1. 其他
	1. 停止web服务方法：在当前启动窗口按ctrl+C
	1. 访问http://ip:3000/
	1. 初始用户名/密码：admin/admin

1. Redmine插件的安装
	1. 把插件复制到 #{RAILS_ROOT}/plugins (Redmine 2.x) or #{RAILS_ROOT}/vendor/plugins (Redmine 1.x) 目录下面。如果你要从 Github 下载插件，你也可以直接进入插件目录，执行下面一条命令：
		git clone git://github.com/user_name/name_of_the_plugin.git
	1. 如果插件需要数据迁移，执行以下命令来升级你的数据库（安全起见，事先备份一下数据库）
			rake redmine:plugins:migrate RAILS_ENV=production
	1. 重启Redmine
		现在你可以在插件列表（管理 -> 插件）中看到刚安装的插件，如果插件需要配置，在这里可以对新插件进行配置。

1. 卸载插件
	1. 如果插件需要迁移，运行以下命令来降级数据库（安全起见，事先备份一下数据库）
			rake redmine:plugins:migrate NAME=plugin_name VERSION=0 RAILS_ENV=production
	1. 从插件目录#{RAILS_ROOT}/plugins删除插件
	1. 重启Redmine

1. Redmine常用插件
	[插件官方列表](http://www.redmine.org/plugins?page=1)
	1. projects_tree_view插件，将项目按照父子关系，整理程属性结构
	1. redmine_attach_screenshot上传截图插件
	1. redmine_ckeditor ，redmine中的ckeditor插件，高级功能插件
	1. redmine_ezlibrarian redmine中的图书、设备管理插件
	1. redmine_importer redmine用户以及bug导入插件
	1. redmine_code_review redmine的用户代码审查插件
	1. timesheet_plugin 工时单插件，可以方便查看各个人的各个项目的工时情况
	1. google_anayltics_plugin 支持第三方统计的插件，可用湿i用google或者其他插件
	1. redmine_last_messages 显示论坛中最新发言或者回复的文件清单
	1. ezfaq_plugin 支持faq功能
	1. advanced_roadmap redmine高级路线图插件，可以方便的知道那个版本的实现时间的