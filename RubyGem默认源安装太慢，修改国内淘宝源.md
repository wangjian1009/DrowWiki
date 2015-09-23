# WHY?
由于国内网络原因（你懂的），导致 rubygems.org 存放在 Amazon S3 上面的资源文件间歇性连接失败。所以你会与遇到 gem install rack 或 bundle install 的时候半天没有响应，具体可以用 gem install rails -V 来查看执行过程。
    
# HOW?
	$ gem sources --remove https://rubygems.org/
	$ gem sources -a http://ruby.taobao.org/
	$ gem sources -l
	*** CURRENT SOURCES ***
	http://ruby.taobao.org
	# 请确保只有 ruby.taobao.org
	$ gem install rails
    
如果是用 Bundle (Rails 项目)
	$ vi Gemfile
	source 'http://ruby.taobao.org/'
	gem 'rails', '3.2.12'
	...
    
# RVM 改用淘宝下载源, 提高 Ruby 安装速度
FOR MAC
	$ sed -i .bak 's!ftp.ruby-lang.org/pub/ruby!ruby.taobao.org/mirrors/ruby!' $rvm_path/config/db
FOR LINUX
	$ sed -i 's!ftp.ruby-lang.org/pub/ruby!ruby.taobao.org/mirrors/ruby!' $rvm_path/config/db