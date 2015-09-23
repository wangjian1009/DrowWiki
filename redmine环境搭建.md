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