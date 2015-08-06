## 拉取项目代码

从远程版本库拉取代码，使用git clone命令，具体格式：

	git clone url
    
但这种方式速度较慢，所以我们一般拷贝一个.git的压缩包到本机解压，然后

在.git文件夹所在的目录执行

	git checkout .

该命令会将本地版本库的内容签出到工作区，但并不包括子模块。

#### 子模块签出：

	git submodule update 子模块名称

目前我们使用的子模块：

    3rdTools
    Game_Flight
    drow

在Game_Flight中，又包含子模块

	FlightRes

依次执行以下命令以获取完整工作区代码和资源：

    git checkout .
    git submodule update drow
    git submodule update Game_Flight
    git submodule update 3rdTools
    cd Game_Flight
    git submodule update FlightRes
    cd FlightRes
    git reset --hard


## 更新代码/资源

每次更新，都必须保证每个工程目录都更新完成。
具体是切换到相应目录下执行更新命令。

必须保证更新或提交的几个目录：
	
	DrowGames		项目Git根目录
	drow			为DrowGames子目录。存放引擎相关代码。
	Game_Flight		DrowGames子目录，存放具体游戏相关代码。
	FlightRes		Game_Flight子目录，存放游戏中使用的资源。


一般情况下，使用

	git pull --rebase

来拉取远程服务器代码
但如果本地有未保存的修改
git会提示，并终止拉取操作

此时根据情况可用不同的方法处理

#### 完全丢弃本地修改

如果完全丢弃工作区的修改，可使用

	git reset --hard

然后执行

	git pull --rebase

#### 保存本地修改（不提交）

这个时候可使用stash命令

	git stash

会将当前工作区改动保存
然后

	git pull --rebase

最后

	git stash pop(apply)

最后一步会执行合并操作。
如果有冲突，需要手动解决冲突内容

#### 部分保存

所做的修改，如果只需要保存一部分
咋可以将需要保存的那一部分

	git add 需要保存的

然后执行

	git checkout .

最后

	git pull --rebase
 
## 提交

#### 全部提交

    git add .
    git commit -m "log msg"
    git pull --rebase
    git push

#### 提交部分
比如现在工作区的修改有
1.txt
2.txt
3.txt

现在需要提交1.2.txt，并保留3.txt的修改
可以以这样

    //将所有修改保存到暂存区
    git add .
    //将3.txt移出暂存区
    git reset 3.txt
    //将暂存区内容（1.txt和2.txt)提交到本地版本库
    git commit -m "edit txt"
    //保存本地工作区修改（只有3.txt了）
    git stash
    //拉取远程版本库
    git pull --rebase
    //将本地版本库修改提交到远程版本库
    git push
    //恢复工作区修改内容
    git stash pop


在提交过程中

	git pull --rebase
    
可能会出现合并冲突
这时需要手动打开文件
修复冲突
然后执行

    git add .
    git rebase --continue
    git push

即可

## 撤销上一次提交

	git reset HEAD^1

此命令用于提交后产生一列问题，或者错误提交
想撤销本次提交

## 拉取远程更新到本地

	git fetch